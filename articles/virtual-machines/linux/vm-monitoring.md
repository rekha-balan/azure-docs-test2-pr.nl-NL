---
title: Enable or Disabling Azure VM Monitoring
description: Describes How to Enable or Disable Azure VM Monitoring
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: ''
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 94108ce7f9a774337a308e1bb6da3e78caf5b5f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551690"
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="a2166-103">Enable or Disable Azure VM Monitoring</span><span class="sxs-lookup"><span data-stu-id="a2166-103">Enable or Disable Azure VM Monitoring</span></span>
<span data-ttu-id="a2166-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span><span class="sxs-lookup"><span data-stu-id="a2166-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="a2166-105">By default monitoring is enabled on Azure Virtual machines if deployed from the [Azure portal](https://portal.azure.com) and monitoring graphs are provided by default with a 1-minute period.</span><span class="sxs-lookup"><span data-stu-id="a2166-105">By default monitoring is enabled on Azure Virtual machines if deployed from the [Azure portal](https://portal.azure.com) and monitoring graphs are provided by default with a 1-minute period.</span></span> <span data-ttu-id="a2166-106">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="a2166-106">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span> 

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="a2166-107">Enable / Disable Monitoring through the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2166-107">Enable / Disable Monitoring through the Azure Portal</span></span>
<span data-ttu-id="a2166-108">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span><span class="sxs-lookup"><span data-stu-id="a2166-108">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="a2166-109">(storage changes apply).</span><span class="sxs-lookup"><span data-stu-id="a2166-109">(storage changes apply).</span></span> <span data-ttu-id="a2166-110">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span><span class="sxs-lookup"><span data-stu-id="a2166-110">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="a2166-111">By default, Azure portal enables monitoring, but you can turn it off as described below.</span><span class="sxs-lookup"><span data-stu-id="a2166-111">By default, Azure portal enables monitoring, but you can turn it off as described below.</span></span> <span data-ttu-id="a2166-112">You can enable monitoring while the VM is running or in stopped state.</span><span class="sxs-lookup"><span data-stu-id="a2166-112">You can enable monitoring while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="a2166-113">Open the Azure portal at **[https://portal.azure.com](https://portal.azure.com)**</span><span class="sxs-lookup"><span data-stu-id="a2166-113">Open the Azure portal at **[https://portal.azure.com](https://portal.azure.com)**</span></span>
* <span data-ttu-id="a2166-114">In the left navigation, click Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a2166-114">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="a2166-115">In the list Virtual machines, select a running or stopped instance.</span><span class="sxs-lookup"><span data-stu-id="a2166-115">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="a2166-116">Virtual machine blad will open.</span><span class="sxs-lookup"><span data-stu-id="a2166-116">Virtual machine blad will open.</span></span>
* <span data-ttu-id="a2166-117">Click "All settings".</span><span class="sxs-lookup"><span data-stu-id="a2166-117">Click "All settings".</span></span>
* <span data-ttu-id="a2166-118">Click "Diagnostics".</span><span class="sxs-lookup"><span data-stu-id="a2166-118">Click "Diagnostics".</span></span>
* <span data-ttu-id="a2166-119">Change status to On or Off.</span><span class="sxs-lookup"><span data-stu-id="a2166-119">Change status to On or Off.</span></span> <span data-ttu-id="a2166-120">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a2166-120">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

[Azure.Note] <span data-ttu-id="a2166-121">The Diagnostics On switch is the default when you create a new virtual machine</span><span class="sxs-lookup"><span data-stu-id="a2166-121">The Diagnostics On switch is the default when you create a new virtual machine</span></span>

![Enable / Disable Monitoring through the Azure Portal.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="a2166-123">Enable / Disable Monitoring with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a2166-123">Enable / Disable Monitoring with Azure CLI</span></span>
<span data-ttu-id="a2166-124">To enable monitoring for an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="a2166-124">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="a2166-125">Create a file named such as PrivateConfig.json with the following content.</span><span class="sxs-lookup"><span data-stu-id="a2166-125">Create a file named such as PrivateConfig.json with the following content.</span></span>
        <span data-ttu-id="a2166-126">{ "storageAccountName":"the storage account to receive data", "storageAccountKey":"the key of the account" }</span><span class="sxs-lookup"><span data-stu-id="a2166-126">{ "storageAccountName":"the storage account to receive data", "storageAccountKey":"the key of the account" }</span></span>
* <span data-ttu-id="a2166-127">Run the following Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="a2166-127">Run the following Azure CLI command.</span></span>
  
        azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.0 --private-config-path PrivateConfig.json

[Azure.Note] <span data-ttu-id="a2166-128">You can change from version 2.0 to a later version when available.</span><span class="sxs-lookup"><span data-stu-id="a2166-128">You can change from version 2.0 to a later version when available.</span></span> 

<span data-ttu-id="a2166-129">For more details about configuring monitoring metrics and samples, visit the document - \*\*[Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2166-129">For more details about configuring monitoring metrics and samples, visit the document - \*\*[Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/vm-monitoring/portal-enable-disable.png



