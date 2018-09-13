---
title: 'Azure Active Directory Domain Services: Create or select a virtual network | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2cc8e851e960cd1211930a94b9aa7942ad4a57d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550074"
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="d2461-103">Create or select a virtual network for Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="d2461-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="d2461-104">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d2461-104">Before you begin</span></span>
<span data-ttu-id="d2461-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="d2461-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="d2461-106">Task 2: Create an Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="d2461-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="d2461-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span><span class="sxs-lookup"><span data-stu-id="d2461-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="d2461-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span><span class="sxs-lookup"><span data-stu-id="d2461-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="d2461-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="d2461-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="d2461-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d2461-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="d2461-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="d2461-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="d2461-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span><span class="sxs-lookup"><span data-stu-id="d2461-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="d2461-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span><span class="sxs-lookup"><span data-stu-id="d2461-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="d2461-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d2461-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d2461-115">In the left pane, select **Networks**.</span><span class="sxs-lookup"><span data-stu-id="d2461-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="d2461-116">![Networks node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="d2461-116">![Networks node](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="d2461-117">The **Virtual Networks** window opens.</span><span class="sxs-lookup"><span data-stu-id="d2461-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="d2461-118">In the task pane at the bottom of the window, click **New**.</span><span class="sxs-lookup"><span data-stu-id="d2461-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Virtual Networks window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="d2461-120">Click **Network Services**, and then select **Virtual Network**.</span><span class="sxs-lookup"><span data-stu-id="d2461-120">Click **Network Services**, and then select **Virtual Network**.</span></span>
    
    ![Virtual network - quick create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="d2461-122">To create a virtual network, click **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="d2461-122">To create a virtual network, click **Quick Create**.</span></span>
    
6. <span data-ttu-id="d2461-123">Specify a **Name** for your virtual network, and consider doing the following:</span><span class="sxs-lookup"><span data-stu-id="d2461-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span> 
    * <span data-ttu-id="d2461-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span><span class="sxs-lookup"><span data-stu-id="d2461-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span> 
    * <span data-ttu-id="d2461-125">You can leave the **DNS server** setting as **None** for now.</span><span class="sxs-lookup"><span data-stu-id="d2461-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="d2461-126">You can update the setting after you enable Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d2461-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="d2461-127">In the **Location** drop-down list, select a supported Azure region.</span><span class="sxs-lookup"><span data-stu-id="d2461-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="d2461-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="d2461-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="d2461-129">To create your virtual network, click **Create a Virtual Network**.</span><span class="sxs-lookup"><span data-stu-id="d2461-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Create a virtual network for Azure Active Directory Domain Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="d2461-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="d2461-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![Create a subnet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="d2461-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="d2461-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span> 

    ![Create a subnet for Azure Active Directory Domain Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="d2461-135">To create the subnet, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d2461-135">To create the subnet, click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2461-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2461-136">Next steps</span></span>
<span data-ttu-id="d2461-137">Task 3: [Enable Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)</span><span class="sxs-lookup"><span data-stu-id="d2461-137">Task 3: [Enable Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)</span></span>






