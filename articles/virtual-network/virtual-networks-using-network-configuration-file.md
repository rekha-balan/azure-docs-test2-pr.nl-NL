---
title: Configure an Azure Virtual Network (Classic) - Network configuration file | Microsoft Docs
description: Learn how to modify virtual networks (Classic) by exporting, changing, and importing a network configuration file using the Azure portal (Classic).
services: virtual-network
documentationcenter: ''
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3827dc0958c51fa0c4ecb1a2e8e3b7bbed42a75a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670143"
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="c3a45-103">Configure a virtual network (Classic) using a network configuration file</span><span class="sxs-lookup"><span data-stu-id="c3a45-103">Configure a virtual network (Classic) using a network configuration file</span></span>
<span data-ttu-id="c3a45-104">You can configure a virtual network (Classic) by using the Azure portal (Classic), or by using a network configuration file.</span><span class="sxs-lookup"><span data-stu-id="c3a45-104">You can configure a virtual network (Classic) by using the Azure portal (Classic), or by using a network configuration file.</span></span> <span data-ttu-id="c3a45-105">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span><span class="sxs-lookup"><span data-stu-id="c3a45-105">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="c3a45-106">You also cannot use the Azure portal to create or modify a virtual network (Classic).</span><span class="sxs-lookup"><span data-stu-id="c3a45-106">You also cannot use the Azure portal to create or modify a virtual network (Classic).</span></span>

## <a name="creating-and-modifying-a-network-configuration-file"></a><span data-ttu-id="c3a45-107">Creating and modifying a network configuration file</span><span class="sxs-lookup"><span data-stu-id="c3a45-107">Creating and modifying a network configuration file</span></span>
<span data-ttu-id="c3a45-108">The easiest way to author a network configuration file is to export the network settings from an existing virtual network (Classic) configuration, then modify the file to contain the settings that you want to configure for your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c3a45-108">The easiest way to author a network configuration file is to export the network settings from an existing virtual network (Classic) configuration, then modify the file to contain the settings that you want to configure for your virtual networks.</span></span>

<span data-ttu-id="c3a45-109">To edit the network configuration file, you can simply open the file, make the appropriate changes, then save the file.</span><span class="sxs-lookup"><span data-stu-id="c3a45-109">To edit the network configuration file, you can simply open the file, make the appropriate changes, then save the file.</span></span> <span data-ttu-id="c3a45-110">You can use any *xml* editor to make changes to the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="c3a45-110">You can use any *xml* editor to make changes to the network configuration file.</span></span> 

<span data-ttu-id="c3a45-111">You should closely follow the guidance for [network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3a45-111">You should closely follow the guidance for [network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

<span data-ttu-id="c3a45-112">Azure considers a subnet that has something deployed to it as **in use**.</span><span class="sxs-lookup"><span data-stu-id="c3a45-112">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="c3a45-113">When a subnet is in use, it cannot be modified.</span><span class="sxs-lookup"><span data-stu-id="c3a45-113">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="c3a45-114">Before modifying, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span><span class="sxs-lookup"><span data-stu-id="c3a45-114">Before modifying, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span>   <span data-ttu-id="c3a45-115">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="c3a45-115">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md).</span></span>

## <a name="export-and-import-virtual-network-settings-using-the-azure-portal-classic"></a><span data-ttu-id="c3a45-116">Export and import virtual network settings using the Azure portal (Classic)</span><span class="sxs-lookup"><span data-stu-id="c3a45-116">Export and import virtual network settings using the Azure portal (Classic)</span></span>
<span data-ttu-id="c3a45-117">You can import and export network configuration settings contained in your network configuration file by using PowerShell or the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="c3a45-117">You can import and export network configuration settings contained in your network configuration file by using PowerShell or the Management Portal.</span></span> <span data-ttu-id="c3a45-118">The instructions below will help you export and import using the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="c3a45-118">The instructions below will help you export and import using the Management Portal.</span></span> 

### <a name="to-export-your-network-settings"></a><span data-ttu-id="c3a45-119">To export your network settings</span><span class="sxs-lookup"><span data-stu-id="c3a45-119">To export your network settings</span></span>
<span data-ttu-id="c3a45-120">When you export, all of the settings for the virtual networks in your subscription will be written to an .xml file.</span><span class="sxs-lookup"><span data-stu-id="c3a45-120">When you export, all of the settings for the virtual networks in your subscription will be written to an .xml file.</span></span> 

1. <span data-ttu-id="c3a45-121">Log into the [Azure portal (Classic)](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c3a45-121">Log into the [Azure portal (Classic)](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="c3a45-122">In the portal, on the bottom of the **networks** page, click **Export**.</span><span class="sxs-lookup"><span data-stu-id="c3a45-122">In the portal, on the bottom of the **networks** page, click **Export**.</span></span> 
3. <span data-ttu-id="c3a45-123">On the **Export network configuration** window, verify that you have selected the subscription for which you want to export your network settings.</span><span class="sxs-lookup"><span data-stu-id="c3a45-123">On the **Export network configuration** window, verify that you have selected the subscription for which you want to export your network settings.</span></span> <span data-ttu-id="c3a45-124">Then, click the checkmark on the lower right.</span><span class="sxs-lookup"><span data-stu-id="c3a45-124">Then, click the checkmark on the lower right.</span></span> 
4. <span data-ttu-id="c3a45-125">When you are prompted, save the *NetworkConfig.xml* file to the location of your choice.</span><span class="sxs-lookup"><span data-stu-id="c3a45-125">When you are prompted, save the *NetworkConfig.xml* file to the location of your choice.</span></span>

### <a name="to-import-your-network-settings"></a><span data-ttu-id="c3a45-126">To import your network settings</span><span class="sxs-lookup"><span data-stu-id="c3a45-126">To import your network settings</span></span>
1. <span data-ttu-id="c3a45-127">In the portal, in the navigation pane on the bottom left, click **New**.</span><span class="sxs-lookup"><span data-stu-id="c3a45-127">In the portal, in the navigation pane on the bottom left, click **New**.</span></span>
2. <span data-ttu-id="c3a45-128">Click **Network Services** -> **Virtual Network** -> **Import Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c3a45-128">Click **Network Services** -> **Virtual Network** -> **Import Configuration**.</span></span>
3. <span data-ttu-id="c3a45-129">On the **Import the network configuration file** page, browse to your network configuration file, and then click the **next** arrow.</span><span class="sxs-lookup"><span data-stu-id="c3a45-129">On the **Import the network configuration file** page, browse to your network configuration file, and then click the **next** arrow.</span></span>
4. <span data-ttu-id="c3a45-130">On the **Building your network** page, you'll see information on the screen showing which sections of your network configuration will be changed or created.</span><span class="sxs-lookup"><span data-stu-id="c3a45-130">On the **Building your network** page, you'll see information on the screen showing which sections of your network configuration will be changed or created.</span></span> <span data-ttu-id="c3a45-131">If the changes look correct to you, click the check mark to proceed to update or create your virtual network.</span><span class="sxs-lookup"><span data-stu-id="c3a45-131">If the changes look correct to you, click the check mark to proceed to update or create your virtual network.</span></span> 

