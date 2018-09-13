---
title: Create an Azure virtual network (classic) - Classic portal | Microsoft Docs
description: Learn how to create a virtual network (classic) with a netcfg file in the Azure classic portal.
services: virtual-network
documentationcenter: ''
author: jimdial
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 69894a0b-8050-451e-8a25-c513e1bd271e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: jdial
ms.openlocfilehash: aab591c09700a7dfb2bcd0bea9a344ab2825a54d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552697"
---
# <a name="create-a-virtual-network-classic-with-a-netcfg-file-using-the-azure-classic-portal"></a><span data-ttu-id="d5324-103">Create a virtual network (classic) with a netcfg file using the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d5324-103">Create a virtual network (classic) with a netcfg file using the Azure classic portal</span></span>
[!INCLUDE [virtual-networks-create-vnet-selectors-classic-include](../../includes/virtual-networks-create-vnet-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d5324-104">This article explains how to create a virtual network with a netcfg file through the classic deployment model using the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="d5324-104">This article explains how to create a virtual network with a netcfg file through the classic deployment model using the Azure classic portal.</span></span> <span data-ttu-id="d5324-105">You can also [create a virtual network through the classic deployment model without using a netcfg file](virtual-networks-create-vnet-classic-pportal.md) or [create a virtual network through the Azure Resource Manager deployment model](virtual-networks-create-vnet-arm-pportal.md) using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d5324-105">You can also [create a virtual network through the classic deployment model without using a netcfg file](virtual-networks-create-vnet-classic-pportal.md) or [create a virtual network through the Azure Resource Manager deployment model](virtual-networks-create-vnet-arm-pportal.md) using the Azure portal.</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="how-to-create-a-vnet-with-a-network-config-file-in-the-microsoft-azure-classic-portal"></a><span data-ttu-id="d5324-106">How to create a VNet with a network config file in the Microsoft Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d5324-106">How to create a VNet with a network config file in the Microsoft Azure classic portal</span></span>
<span data-ttu-id="d5324-107">Azure uses an xml file to define all VNets available to a subscription.</span><span class="sxs-lookup"><span data-stu-id="d5324-107">Azure uses an xml file to define all VNets available to a subscription.</span></span> <span data-ttu-id="d5324-108">You can download this file and edit it to create VNets through the classic deployment model or to modify or delete existing VNets.</span><span class="sxs-lookup"><span data-stu-id="d5324-108">You can download this file and edit it to create VNets through the classic deployment model or to modify or delete existing VNets.</span></span> <span data-ttu-id="d5324-109">This article explains how to download this file, referred to as a network configuration (or netcfg) file, add a VNet to it, and upload the file to create the VNet.</span><span class="sxs-lookup"><span data-stu-id="d5324-109">This article explains how to download this file, referred to as a network configuration (or netcfg) file, add a VNet to it, and upload the file to create the VNet.</span></span> <span data-ttu-id="d5324-110">To learn more about the network configuration file, review the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5324-110">To learn more about the network configuration file, review the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="d5324-111">To create a VNet using a netcfg file through the Azure classic portal, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="d5324-111">To create a VNet using a netcfg file through the Azure classic portal, complete the following steps:</span></span>

1. <span data-ttu-id="d5324-112">From a browser, navigate to http://manage.windowsazure.com and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="d5324-112">From a browser, navigate to http://manage.windowsazure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="d5324-113">Scroll down the list of services, click **NETWORKS**, then **EXPORT**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="d5324-113">Scroll down the list of services, click **NETWORKS**, then **EXPORT**, as shown in the following picture:</span></span>

    ![Azure virtual networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-classic-portal/networks.png)
3. <span data-ttu-id="d5324-115">In the **Export network configuration** dialog box, select the subscription you want to export the virtual network configuration from, then click the check mark button at the bottom-right corner of the box.</span><span class="sxs-lookup"><span data-stu-id="d5324-115">In the **Export network configuration** dialog box, select the subscription you want to export the virtual network configuration from, then click the check mark button at the bottom-right corner of the box.</span></span>
4. <span data-ttu-id="d5324-116">Follow your browser instructions to save the **NetworkConfig.xml** file.</span><span class="sxs-lookup"><span data-stu-id="d5324-116">Follow your browser instructions to save the **NetworkConfig.xml** file.</span></span> <span data-ttu-id="d5324-117">Make sure you note where you are saving the file.</span><span class="sxs-lookup"><span data-stu-id="d5324-117">Make sure you note where you are saving the file.</span></span>
5. <span data-ttu-id="d5324-118">Open the file you saved in step 4 using any XML or text editor application, and look for the `<VirtualNetworkSites>` element within the `<VirtualNetworkConfiguration>` element.</span><span class="sxs-lookup"><span data-stu-id="d5324-118">Open the file you saved in step 4 using any XML or text editor application, and look for the `<VirtualNetworkSites>` element within the `<VirtualNetworkConfiguration>` element.</span></span> <span data-ttu-id="d5324-119">If you have any existing VNets, each is listed in its own `<VirtualNetworkSite>` element.</span><span class="sxs-lookup"><span data-stu-id="d5324-119">If you have any existing VNets, each is listed in its own `<VirtualNetworkSite>` element.</span></span> <span data-ttu-id="d5324-120">If the file does not contain a `<VirtualNetworkSites>` element within the `<VirtualNetworkConfiguration>` element, create one.</span><span class="sxs-lookup"><span data-stu-id="d5324-120">If the file does not contain a `<VirtualNetworkSites>` element within the `<VirtualNetworkConfiguration>` element, create one.</span></span>
6. <span data-ttu-id="d5324-121">If your existing NetworkConfig file doesn't have any VNets in it, your NetworkConfig.xml file will resemble the following example after you add the VNet described in this scenario to it:</span><span class="sxs-lookup"><span data-stu-id="d5324-121">If your existing NetworkConfig file doesn't have any VNets in it, your NetworkConfig.xml file will resemble the following example after you add the VNet described in this scenario to it:</span></span>

    ```xml
    <NetworkConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="TestVNet" Location="Central US">
            <AddressSpace>
              <AddressPrefix>192.168.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>192.168.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>192.168.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>
    ```
7. <span data-ttu-id="d5324-122">Save the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="d5324-122">Save the network configuration file.</span></span>
8. <span data-ttu-id="d5324-123">In the Azure classic portal, click **NEW**, **NETWORK SERVICES**, **VIRTUAL NETWORK**, and click **IMPORT CONFIGURATION** as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="d5324-123">In the Azure classic portal, click **NEW**, **NETWORK SERVICES**, **VIRTUAL NETWORK**, and click **IMPORT CONFIGURATION** as shown in the following picture:</span></span>

    ![Import configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-classic-portal/import.png)
10. <span data-ttu-id="d5324-125">In the **Import the network configuration file** dialog box, click **BROWSE FOR FILE...**, navigate to the folder you saved the file to in step 7, select the file, and click **Open**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="d5324-125">In the **Import the network configuration file** dialog box, click **BROWSE FOR FILE...**, navigate to the folder you saved the file to in step 7, select the file, and click **Open**, as shown in the following picture:</span></span>

    ![Import network configuration file page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-classic-portal/vnet-create-portal-netcfg-figure4.png)

    <span data-ttu-id="d5324-127">In the bottom-right corner of the box, click the arrow button to move to the next step.</span><span class="sxs-lookup"><span data-stu-id="d5324-127">In the bottom-right corner of the box, click the arrow button to move to the next step.</span></span>

9. <span data-ttu-id="d5324-128">In the **Building your network** dialog box, notice the entry for the new VNet, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="d5324-128">In the **Building your network** dialog box, notice the entry for the new VNet, as shown in the following picture:</span></span>

    ![Building your network page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-classic-portal/vnet-create-portal-netcfg-figure5.png)
10. <span data-ttu-id="d5324-130">To create the VNet, click the check mark button in the bottom-right corner of the box in the previous picture.</span><span class="sxs-lookup"><span data-stu-id="d5324-130">To create the VNet, click the check mark button in the bottom-right corner of the box in the previous picture.</span></span> <span data-ttu-id="d5324-131">After a few seconds the VNet appears in the list of available VNets, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="d5324-131">After a few seconds the VNet appears in the list of available VNets, as shown in the following picture:</span></span>

    ![New virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-create-vnet-classic-portal/vnet-create-portal-netcfg-figure6.png)





