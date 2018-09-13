---
title: Troubleshoot creating RemoteApp hybrid collections | Microsoft Docs
description: Learn how to troubleshoot RemoteApp hybrid collection creation failures
services: remoteapp
documentationcenter: ''
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: ffefe300fdc87faee01bb98ffe730aa7bb8d3ac7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549476"
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="3d682-103">Troubleshoot creating Azure RemoteApp hybrid collections</span><span class="sxs-lookup"><span data-stu-id="3d682-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3d682-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="3d682-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3d682-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="3d682-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3d682-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span><span class="sxs-lookup"><span data-stu-id="3d682-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="3d682-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d682-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="3d682-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="3d682-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="3d682-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3d682-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="3d682-110">Haven't created your collection yet?</span><span class="sxs-lookup"><span data-stu-id="3d682-110">Haven't created your collection yet?</span></span> <span data-ttu-id="3d682-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span><span class="sxs-lookup"><span data-stu-id="3d682-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="3d682-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span><span class="sxs-lookup"><span data-stu-id="3d682-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="3d682-113">Your image is invalid</span><span class="sxs-lookup"><span data-stu-id="3d682-113">Your image is invalid</span></span>
<span data-ttu-id="3d682-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="3d682-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="3d682-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span><span class="sxs-lookup"><span data-stu-id="3d682-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="3d682-116">Does your VNET have network security groups defined?</span><span class="sxs-lookup"><span data-stu-id="3d682-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="3d682-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span><span class="sxs-lookup"><span data-stu-id="3d682-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="3d682-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span><span class="sxs-lookup"><span data-stu-id="3d682-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="3d682-119">Are you using your own DNS servers?</span><span class="sxs-lookup"><span data-stu-id="3d682-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="3d682-120">And are they accessible from your VNET subnet?</span><span class="sxs-lookup"><span data-stu-id="3d682-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="3d682-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span><span class="sxs-lookup"><span data-stu-id="3d682-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="3d682-122">Don't use Google DNS for this.</span><span class="sxs-lookup"><span data-stu-id="3d682-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="3d682-123">For hybrid collections you use your own DNS servers.</span><span class="sxs-lookup"><span data-stu-id="3d682-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="3d682-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span><span class="sxs-lookup"><span data-stu-id="3d682-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="3d682-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span><span class="sxs-lookup"><span data-stu-id="3d682-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="3d682-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span><span class="sxs-lookup"><span data-stu-id="3d682-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="3d682-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span><span class="sxs-lookup"><span data-stu-id="3d682-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="3d682-128">For example:</span><span class="sxs-lookup"><span data-stu-id="3d682-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Define your DNS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="3d682-130">Are you using an Active Directory domain controller in your collection?</span><span class="sxs-lookup"><span data-stu-id="3d682-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="3d682-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3d682-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="3d682-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span><span class="sxs-lookup"><span data-stu-id="3d682-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="3d682-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span><span class="sxs-lookup"><span data-stu-id="3d682-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="3d682-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="3d682-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="3d682-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span><span class="sxs-lookup"><span data-stu-id="3d682-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="3d682-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span><span class="sxs-lookup"><span data-stu-id="3d682-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="3d682-137">What domain name did you specify when you created your collection?</span><span class="sxs-lookup"><span data-stu-id="3d682-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="3d682-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span><span class="sxs-lookup"><span data-stu-id="3d682-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="3d682-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span><span class="sxs-lookup"><span data-stu-id="3d682-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>


