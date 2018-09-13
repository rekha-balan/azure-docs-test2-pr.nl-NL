---
title: Enable FTP in App Service on Azure Stack | Microsoft Docs
description: Steps to complete to enable FTP in App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 51e1ea880da43741a8042be46c9b6e6408ceb23e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553673"
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a><span data-ttu-id="e41cf-103">Enable FTP in App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e41cf-103">Enable FTP in App Service on Azure Stack</span></span>

<span data-ttu-id="e41cf-104">Once you have successfully deployed App Service on Azure Stack if you wish to enable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need to be completed.</span><span class="sxs-lookup"><span data-stu-id="e41cf-104">Once you have successfully deployed App Service on Azure Stack if you wish to enable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need to be completed.</span></span>  <span data-ttu-id="e41cf-105">In future releases these steps will be automated.</span><span class="sxs-lookup"><span data-stu-id="e41cf-105">In future releases these steps will be automated.</span></span>

> [!NOTE]
> <span data-ttu-id="e41cf-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="e41cf-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span></span>

## <a name="enable-ftp"></a><span data-ttu-id="e41cf-107">Enable FTP</span><span class="sxs-lookup"><span data-stu-id="e41cf-107">Enable FTP</span></span>

1.  <span data-ttu-id="e41cf-108">Log in to the Azure Stack portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="e41cf-108">Log in to the Azure Stack portal as the service administrator.</span></span>
2.  <span data-ttu-id="e41cf-109">Browse to **Network interfaces** and select the **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="e41cf-109">Browse to **Network interfaces** and select the **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span></span> <span data-ttu-id="e41cf-110">![Azure Stack Network Interfaces][1]</span><span class="sxs-lookup"><span data-stu-id="e41cf-110">![Azure Stack Network Interfaces][1]</span></span>
3.  <span data-ttu-id="e41cf-111">Note the **Public IP Address** of the **FTP-NIC**.</span><span class="sxs-lookup"><span data-stu-id="e41cf-111">Note the **Public IP Address** of the **FTP-NIC**.</span></span> <span data-ttu-id="e41cf-112">![Azure Stack Network Interface Details][2]</span><span class="sxs-lookup"><span data-stu-id="e41cf-112">![Azure Stack Network Interface Details][2]</span></span>
4.  <span data-ttu-id="e41cf-113">Next Browse to **Virtual Machines** and select the **FTP0-VM**.</span><span class="sxs-lookup"><span data-stu-id="e41cf-113">Next Browse to **Virtual Machines** and select the **FTP0-VM**.</span></span> <span data-ttu-id="e41cf-114">![Azure Stack Virtual Machines][3]</span><span class="sxs-lookup"><span data-stu-id="e41cf-114">![Azure Stack Virtual Machines][3]</span></span>
5.  <span data-ttu-id="e41cf-115">Open a remote desktop session to the VM using the **Connect** button and login to the session using the Administrator credentials you set during App Service deployment.</span><span class="sxs-lookup"><span data-stu-id="e41cf-115">Open a remote desktop session to the VM using the **Connect** button and login to the session using the Administrator credentials you set during App Service deployment.</span></span>  
<span data-ttu-id="e41cf-116">![Azure Stack Virtual Machine Details][4]</span><span class="sxs-lookup"><span data-stu-id="e41cf-116">![Azure Stack Virtual Machine Details][4]</span></span>
6.  <span data-ttu-id="e41cf-117">Open **Internet Information Service (IIS) Manager** on the FTP VM (FTP0-VM).</span><span class="sxs-lookup"><span data-stu-id="e41cf-117">Open **Internet Information Service (IIS) Manager** on the FTP VM (FTP0-VM).</span></span>
7.  <span data-ttu-id="e41cf-118">Under **Sites** select **Hosting FTP Site**.</span><span class="sxs-lookup"><span data-stu-id="e41cf-118">Under **Sites** select **Hosting FTP Site**.</span></span>
8.  <span data-ttu-id="e41cf-119">Open **FTP Firewall Support**.</span><span class="sxs-lookup"><span data-stu-id="e41cf-119">Open **FTP Firewall Support**.</span></span> <span data-ttu-id="e41cf-120">![IIS Manager on App Service FTP0-VM][5]</span><span class="sxs-lookup"><span data-stu-id="e41cf-120">![IIS Manager on App Service FTP0-VM][5]</span></span>
9.  <span data-ttu-id="e41cf-121">Enter the Public IP Address of the FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span><span class="sxs-lookup"><span data-stu-id="e41cf-121">Enter the Public IP Address of the FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span></span>

## <a name="validate-the-enabling-of-ftp"></a><span data-ttu-id="e41cf-122">Validate the enabling of FTP</span><span class="sxs-lookup"><span data-stu-id="e41cf-122">Validate the enabling of FTP</span></span>

1.  <span data-ttu-id="e41cf-123">Log in to the Azure Stack portal as either the service administrator or as a tenant.</span><span class="sxs-lookup"><span data-stu-id="e41cf-123">Log in to the Azure Stack portal as either the service administrator or as a tenant.</span></span>
2.  <span data-ttu-id="e41cf-124">Browse to **App Services** and select a Web, Mobile, or API App you have created.</span><span class="sxs-lookup"><span data-stu-id="e41cf-124">Browse to **App Services** and select a Web, Mobile, or API App you have created.</span></span> <span data-ttu-id="e41cf-125">![App Services][7]</span><span class="sxs-lookup"><span data-stu-id="e41cf-125">![App Services][7]</span></span>
3.  <span data-ttu-id="e41cf-126">In the application details note the **FTP Hostname** and **FTP/deployment username**.</span><span class="sxs-lookup"><span data-stu-id="e41cf-126">In the application details note the **FTP Hostname** and **FTP/deployment username**.</span></span> <span data-ttu-id="e41cf-127">![App Service App Details][8]</span><span class="sxs-lookup"><span data-stu-id="e41cf-127">![App Service App Details][8]</span></span>
> [!NOTE]
> <span data-ttu-id="e41cf-128">If you do not see an entry under **FTP/deployment username**, you need to set the Deployment credentials first using the **Deployment Credentials** Blade.</span><span class="sxs-lookup"><span data-stu-id="e41cf-128">If you do not see an entry under **FTP/deployment username**, you need to set the Deployment credentials first using the **Deployment Credentials** Blade.</span></span>

4.  <span data-ttu-id="e41cf-129">Open Windows Explorer, enter the FTP hostname into the file address bar for example, ftp://ftp.appservice.azurestack.local</span><span class="sxs-lookup"><span data-stu-id="e41cf-129">Open Windows Explorer, enter the FTP hostname into the file address bar for example, ftp://ftp.appservice.azurestack.local</span></span>
5.  <span data-ttu-id="e41cf-130">When prompted enter the **Deployment credentials** you noted in step 3, if the feature has been enabled you will see a directory listing of the app service application's contents.</span><span class="sxs-lookup"><span data-stu-id="e41cf-130">When prompted enter the **Deployment credentials** you noted in step 3, if the feature has been enabled you will see a directory listing of the app service application's contents.</span></span> <span data-ttu-id="e41cf-131">![FTP File Listing][9] <!--Image references--> [1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png [2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png [3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png [4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png [5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png [6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png [7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png [8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png [9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png</span><span class="sxs-lookup"><span data-stu-id="e41cf-131">![FTP File Listing][9] <!--Image references--> [1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png [2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png [3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png [4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png [5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png [6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png [7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png [8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png [9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png</span></span>









