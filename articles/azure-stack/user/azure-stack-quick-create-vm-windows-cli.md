---
title: Create a Windows virtual machine on Azure Stack using Azure CLI | Microsoft Docs
description: Learn how to create a Windows VM on Azure Stack using Azure CLI
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/10/2018
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: be4e16b1d20aa07e4851174e982e2f1f2a23d893
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968982"
---
# <a name="quickstart-create-a-windows-server-virtual-machine-by-using-azure-cli-in-azure-stack"></a><span data-ttu-id="6c943-103">Quickstart: create a Windows Server virtual machine by using Azure CLI in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6c943-103">Quickstart: create a Windows Server virtual machine by using Azure CLI in Azure Stack</span></span>

<span data-ttu-id="6c943-104">‎*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="6c943-104">‎*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="6c943-105">You can create a Windows Server 2016 virtual machine by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c943-105">You can create a Windows Server 2016 virtual machine by using the Azure CLI.</span></span> <span data-ttu-id="6c943-106">Follow the steps in this article to create and use a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-106">Follow the steps in this article to create and use a virtual machine.</span></span> <span data-ttu-id="6c943-107">This article also gives you the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c943-107">This article also gives you the following steps:</span></span>

* <span data-ttu-id="6c943-108">Connect to the virtual machine with a remote client.</span><span class="sxs-lookup"><span data-stu-id="6c943-108">Connect to the virtual machine with a remote client.</span></span>
* <span data-ttu-id="6c943-109">Install the IIS web server and view the default home page.</span><span class="sxs-lookup"><span data-stu-id="6c943-109">Install the IIS web server and view the default home page.</span></span>
* <span data-ttu-id="6c943-110">Clean up your resources.</span><span class="sxs-lookup"><span data-stu-id="6c943-110">Clean up your resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c943-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c943-111">Prerequisites</span></span>

* <span data-ttu-id="6c943-112">Make sure that your Azure Stack operator added the **Windows Server 2016** image to the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="6c943-112">Make sure that your Azure Stack operator added the **Windows Server 2016** image to the Azure Stack marketplace.</span></span>

* <span data-ttu-id="6c943-113">Azure Stack requires a specific version of Azure CLI to create and manage the resources.</span><span class="sxs-lookup"><span data-stu-id="6c943-113">Azure Stack requires a specific version of Azure CLI to create and manage the resources.</span></span> <span data-ttu-id="6c943-114">If you don't have Azure CLI configured for Azure Stack, follow the steps to [install and configure Azure CLI](azure-stack-version-profiles-azurecli2.md).</span><span class="sxs-lookup"><span data-stu-id="6c943-114">If you don't have Azure CLI configured for Azure Stack, follow the steps to [install and configure Azure CLI](azure-stack-version-profiles-azurecli2.md).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6c943-115">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="6c943-115">Create a resource group</span></span>

<span data-ttu-id="6c943-116">A resource group is a logical container where you can deploy and manage Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="6c943-116">A resource group is a logical container where you can deploy and manage Azure Stack resources.</span></span> <span data-ttu-id="6c943-117">From your Azure Stack environment, run the [az group create](/cli/azure/group#az-group-create) command to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="6c943-117">From your Azure Stack environment, run the [az group create](/cli/azure/group#az-group-create) command to create a resource group.</span></span>

>[!NOTE]
 <span data-ttu-id="6c943-118">Values are assigned for all the variables in the code examples.</span><span class="sxs-lookup"><span data-stu-id="6c943-118">Values are assigned for all the variables in the code examples.</span></span> <span data-ttu-id="6c943-119">However, you can assign new values if you want to.</span><span class="sxs-lookup"><span data-stu-id="6c943-119">However, you can assign new values if you want to.</span></span>

<span data-ttu-id="6c943-120">The following example creates a resource group named myResourceGroup in the local location.</span><span class="sxs-lookup"><span data-stu-id="6c943-120">The following example creates a resource group named myResourceGroup in the local location.</span></span>

```cli
az group create --name myResourceGroup --location local
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="6c943-121">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="6c943-121">Create a virtual machine</span></span>

<span data-ttu-id="6c943-122">Create a virtual machine (VM) by using the [az vm create](/cli/azure/vm#az-vm-create) command.</span><span class="sxs-lookup"><span data-stu-id="6c943-122">Create a virtual machine (VM) by using the [az vm create](/cli/azure/vm#az-vm-create) command.</span></span> <span data-ttu-id="6c943-123">The following example creates a VM named myVM.</span><span class="sxs-lookup"><span data-stu-id="6c943-123">The following example creates a VM named myVM.</span></span> <span data-ttu-id="6c943-124">This example uses Demouser for an administrative user name and Demouser@123 as the user password.</span><span class="sxs-lookup"><span data-stu-id="6c943-124">This example uses Demouser for an administrative user name and Demouser@123 as the user password.</span></span> <span data-ttu-id="6c943-125">Change these values to something that is appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="6c943-125">Change these values to something that is appropriate for your environment.</span></span>

```cli
az vm create \
  --resource-group "myResourceGroup" \
  --name "myVM" \
  --image "Win2016Datacenter" \
  --admin-username "Demouser" \
  --admin-password "Demouser@123" \
  --use-unmanaged-disk \
  --location local
```

<span data-ttu-id="6c943-126">When the VM is created, the **PublicIPAddress** parameter in the output contains the public IP address for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-126">When the VM is created, the **PublicIPAddress** parameter in the output contains the public IP address for the virtual machine.</span></span> <span data-ttu-id="6c943-127">Write down this address because you need it to access the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-127">Write down this address because you need it to access the virtual machine.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="6c943-128">Open port 80 for web traffic</span><span class="sxs-lookup"><span data-stu-id="6c943-128">Open port 80 for web traffic</span></span>

<span data-ttu-id="6c943-129">Because this VM is going to run the IIS web server, you need to open port 80 to Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="6c943-129">Because this VM is going to run the IIS web server, you need to open port 80 to Internet traffic.</span></span>

<span data-ttu-id="6c943-130">Use the [az vm open-port](/cli/azure/vm#open-port) command to open port 80.</span><span class="sxs-lookup"><span data-stu-id="6c943-130">Use the [az vm open-port](/cli/azure/vm#open-port) command to open port 80.</span></span>

```cli
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="6c943-131">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="6c943-131">Connect to the virtual machine</span></span>

<span data-ttu-id="6c943-132">Use the next command to create a Remote Desktop connection to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-132">Use the next command to create a Remote Desktop connection to your virtual machine.</span></span> <span data-ttu-id="6c943-133">Replace "Public IP Address" with the IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-133">Replace "Public IP Address" with the IP address of your virtual machine.</span></span> <span data-ttu-id="6c943-134">When prompted, enter the username and password that you used for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-134">When prompted, enter the username and password that you used for the virtual machine.</span></span>

```
mstsc /v <Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="6c943-135">Install IIS using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c943-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="6c943-136">Now that you've logged in to the virtual machine, you can use PowerShell to install IIS.</span><span class="sxs-lookup"><span data-stu-id="6c943-136">Now that you've logged in to the virtual machine, you can use PowerShell to install IIS.</span></span> <span data-ttu-id="6c943-137">Start PowerShell on the virtual machine and run the following command:</span><span class="sxs-lookup"><span data-stu-id="6c943-137">Start PowerShell on the virtual machine and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="6c943-138">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="6c943-138">View the IIS welcome page</span></span>

<span data-ttu-id="6c943-139">You can use a web browser of your choice to view the default IIS welcome page.</span><span class="sxs-lookup"><span data-stu-id="6c943-139">You can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="6c943-140">Use the public IP address documented in the previous section to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="6c943-140">Use the public IP address documented in the previous section to visit the default page.</span></span>

![IIS default site](./media/azure-stack-quick-create-vm-windows-cli/default-iis-website.png)

## <a name="clean-up-resources"></a><span data-ttu-id="6c943-142">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6c943-142">Clean up resources</span></span>

<span data-ttu-id="6c943-143">Clean up the resources that you don't need any longer.</span><span class="sxs-lookup"><span data-stu-id="6c943-143">Clean up the resources that you don't need any longer.</span></span> <span data-ttu-id="6c943-144">Use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, the virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="6c943-144">Use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, the virtual machine, and all related resources.</span></span>

```cli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="6c943-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c943-145">Next steps</span></span>

<span data-ttu-id="6c943-146">In this quickstart, you deployed a basic Windows Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6c943-146">In this quickstart, you deployed a basic Windows Server virtual machine.</span></span> <span data-ttu-id="6c943-147">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="6c943-147">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span></span>
