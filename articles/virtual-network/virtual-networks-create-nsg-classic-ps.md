---
title: Create network security groups (Classic) in Azure - PowerShell| Microsoft Docs
description: Learn how to create and deploy NSGs in classic mode using PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 86810b0d-0240-46a2-8548-fca22daa56f3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: cf202a605e5141e7d1fd54790bf6597617c9b97c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555947"
---
# <a name="how-to-create-nsgs-classic-in-powershell"></a><span data-ttu-id="c3628-103">How to create NSGs (classic) in PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3628-103">How to create NSGs (classic) in PowerShell</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c3628-104">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="c3628-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="c3628-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c3628-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="c3628-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="c3628-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="c3628-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c3628-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="c3628-108">How to create the NSG for the front-end subnet</span><span class="sxs-lookup"><span data-stu-id="c3628-108">How to create the NSG for the front-end subnet</span></span>
<span data-ttu-id="c3628-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c3628-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below:</span></span>

1. <span data-ttu-id="c3628-110">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span><span class="sxs-lookup"><span data-stu-id="c3628-110">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="c3628-111">Create a network security group named **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="c3628-111">Create a network security group named **NSG-FrontEnd**.</span></span>
   
        New-AzureNetworkSecurityGroup -Name "NSG-FrontEnd" -Location uswest `
            -Label "Front end subnet NSG"
   
    <span data-ttu-id="c3628-112">Expected output:</span><span class="sxs-lookup"><span data-stu-id="c3628-112">Expected output:</span></span>

        Name         Location   Label               
        
        NSG-FrontEnd West US     Front end subnet NSG

3. <span data-ttu-id="c3628-113">Create a security rule allowing access from the Internet to port 3389.</span><span class="sxs-lookup"><span data-stu-id="c3628-113">Create a security rule allowing access from the Internet to port 3389.</span></span>
   
        Get-AzureNetworkSecurityGroup -Name "NSG-FrontEnd" `
        | Set-AzureNetworkSecurityRule -Name rdp-rule `
            -Action Allow -Protocol TCP -Type Inbound -Priority 100 `
            -SourceAddressPrefix Internet  -SourcePortRange '*' `
            -DestinationAddressPrefix '*' -DestinationPortRange '3389'
   
    <span data-ttu-id="c3628-114">Expected output:</span><span class="sxs-lookup"><span data-stu-id="c3628-114">Expected output:</span></span>
   
        Name     : NSG-FrontEnd
        Location : Central US
        Label    : Front end subnet NSG
        Rules    :
   
                      Type: Inbound
   
                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   rdp-rule             100       Allow    INTERNET        *             *                3389           TCP     
                   ALLOW VNET INBOUND   65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW AZURE LOAD     65001     Allow    AZURE_LOADBALAN *             *                *              *       
                   BALANCER INBOUND                        CER                                                                   
                   DENY ALL INBOUND     65500     Deny     *               *             *                *              *       

                      Type: Outbound

                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   ALLOW VNET OUTBOUND  65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW INTERNET       65001     Allow    *               *             INTERNET         *              *       
                   OUTBOUND                                                                                                      
                   DENY ALL OUTBOUND    65500     Deny     *               *             *                *              *

1. <span data-ttu-id="c3628-115">Create a security rule allowing access from the Internet to port 80.</span><span class="sxs-lookup"><span data-stu-id="c3628-115">Create a security rule allowing access from the Internet to port 80.</span></span>
   
        Get-AzureNetworkSecurityGroup -Name "NSG-FrontEnd" `
        | Set-AzureNetworkSecurityRule -Name web-rule `
            -Action Allow -Protocol TCP -Type Inbound -Priority 200 `
            -SourceAddressPrefix Internet  -SourcePortRange '*' `
            -DestinationAddressPrefix '*' -DestinationPortRange '80'
   
    <span data-ttu-id="c3628-116">Expected output:</span><span class="sxs-lookup"><span data-stu-id="c3628-116">Expected output:</span></span>

        Name     : NSG-FrontEnd
        Location : Central US
        Label    : Front end subnet NSG
        Rules    :

                      Type: Inbound

                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   rdp-rule             100       Allow    INTERNET        *             *                3389           TCP     
                   web-rule             200       Allow    INTERNET        *             *                80             TCP     
                   ALLOW VNET INBOUND   65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW AZURE LOAD     65001     Allow    AZURE_LOADBALAN *             *                *              *       
                   BALANCER INBOUND                        CER                                                                   
                   DENY ALL INBOUND     65500     Deny     *               *             *                *              *       


                      Type: Outbound

                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   ALLOW VNET OUTBOUND  65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW INTERNET       65001     Allow    *               *             INTERNET         *              *       
                   OUTBOUND                                                                                                      
                   DENY ALL OUTBOUND    65500     Deny     *               *             *                *              *   

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="c3628-117">How to create the NSG for the back end subnet</span><span class="sxs-lookup"><span data-stu-id="c3628-117">How to create the NSG for the back end subnet</span></span>
1. <span data-ttu-id="c3628-118">Create a network security group named **NSG-BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="c3628-118">Create a network security group named **NSG-BackEnd**.</span></span>
   
        New-AzureNetworkSecurityGroup -Name "NSG-BackEnd" -Location uswest `
            -Label "Back end subnet NSG"
   
    <span data-ttu-id="c3628-119">Expected output:</span><span class="sxs-lookup"><span data-stu-id="c3628-119">Expected output:</span></span>
   
        Name        Location   Label              
        
        NSG-BackEnd West US    Back end subnet NSG
2. <span data-ttu-id="c3628-120">Create a security rule allowing access from the front end subnet to port 1433 (default port used by SQL Server).</span><span class="sxs-lookup"><span data-stu-id="c3628-120">Create a security rule allowing access from the front end subnet to port 1433 (default port used by SQL Server).</span></span>
   
        Get-AzureNetworkSecurityGroup -Name "NSG-FrontEnd" `
        | Set-AzureNetworkSecurityRule -Name rdp-rule `
            -Action Allow -Protocol TCP -Type Inbound -Priority 100 `
            -SourceAddressPrefix 192.168.1.0/24  -SourcePortRange '*' `
            -DestinationAddressPrefix '*' -DestinationPortRange '1433'
   
    <span data-ttu-id="c3628-121">Expected output:</span><span class="sxs-lookup"><span data-stu-id="c3628-121">Expected output:</span></span>
   
        Name     : NSG-BackEnd
        Location : Central US
        Label    : Back end subnet NSG
        Rules    :
   
                      Type: Inbound
   
                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   fe-rule              100       Allow    192.168.1.0/24  *             *                1433           TCP     
                   ALLOW VNET INBOUND   65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW AZURE LOAD     65001     Allow    AZURE_LOADBALAN *             *                *              *       
                   BALANCER INBOUND                        CER                                                                   
                   DENY ALL INBOUND     65500     Deny     *               *             *                *              *       

                      Type: Outbound

                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   ALLOW VNET OUTBOUND  65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW INTERNET       65001     Allow    *               *             INTERNET         *              *       
                   OUTBOUND                                                                                                      
                   DENY ALL OUTBOUND    65500     Deny     *               *             *                *              *      

1. <span data-ttu-id="c3628-122">Create a security rule blocking access from the subnet to the Internet.</span><span class="sxs-lookup"><span data-stu-id="c3628-122">Create a security rule blocking access from the subnet to the Internet.</span></span>
   
        Get-AzureNetworkSecurityGroup -Name "NSG-BackEnd" `
        | Set-AzureNetworkSecurityRule -Name block-internet `
            -Action Deny -Protocol '*' -Type Outbound -Priority 200 `
            -SourceAddressPrefix '*'  -SourcePortRange '*' `
            -DestinationAddressPrefix Internet -DestinationPortRange '*'
   
    <span data-ttu-id="c3628-123">Expected output:</span><span class="sxs-lookup"><span data-stu-id="c3628-123">Expected output:</span></span>
   
        Name     : NSG-BackEnd
        Location : Central US
        Label    : Back end subnet NSG
        Rules    :
   
                      Type: Inbound
   
                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   fe-rule              100       Allow    192.168.1.0/24  *             *                1433           TCP     
                   ALLOW VNET INBOUND   65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW AZURE LOAD     65001     Allow    AZURE_LOADBALAN *             *                *              *       
                   BALANCER INBOUND                        CER                                                                   
                   DENY ALL INBOUND     65500     Deny     *               *             *                *              *       

                      Type: Outbound

                   Name                 Priority  Action   Source Address  Source Port   Destination      Destination    Protocol
                                                           Prefix          Range         Address Prefix   Port Range             
                   
                   block-internet       200       Deny     *               *             INTERNET         *              *       
                   ALLOW VNET OUTBOUND  65000     Allow    VIRTUAL_NETWORK *             VIRTUAL_NETWORK  *              *       
                   ALLOW INTERNET       65001     Allow    *               *             INTERNET         *              *       
                   OUTBOUND                                                                                                      
                   DENY ALL OUTBOUND    65500     Deny     *               *             *                *              *   
