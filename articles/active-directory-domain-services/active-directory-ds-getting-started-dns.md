---
title: 'Azure Active Directory Domain Services: Update DNS settings for the Azure virtual network | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: a1fab54cc41103aeae0443c3762f798fcf9f4f90
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550742"
---
# <a name="update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="91dfc-103">Update DNS settings for the Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="91dfc-103">Update DNS settings for the Azure virtual network</span></span>
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a><span data-ttu-id="91dfc-104">Task 4: Update DNS settings for the Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="91dfc-104">Task 4: Update DNS settings for the Azure virtual network</span></span>
<span data-ttu-id="91dfc-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span><span class="sxs-lookup"><span data-stu-id="91dfc-105">In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory.</span></span> <span data-ttu-id="91dfc-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span><span class="sxs-lookup"><span data-stu-id="91dfc-106">The next task is to ensure that computers within the virtual network can connect and consume these services.</span></span> <span data-ttu-id="91dfc-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="91dfc-107">In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.</span></span>

> [!NOTE]
> <span data-ttu-id="91dfc-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span><span class="sxs-lookup"><span data-stu-id="91dfc-108">After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.</span></span>
>
>

<span data-ttu-id="91dfc-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, do the following:</span><span class="sxs-lookup"><span data-stu-id="91dfc-109">To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="91dfc-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="91dfc-110">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="91dfc-111">In the left pane, select **Networks**.</span><span class="sxs-lookup"><span data-stu-id="91dfc-111">In the left pane, select **Networks**.</span></span>  
    <span data-ttu-id="91dfc-112">The **Networks** window opens.</span><span class="sxs-lookup"><span data-stu-id="91dfc-112">The **Networks** window opens.</span></span>

    ![Virtual networks window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. <span data-ttu-id="91dfc-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span><span class="sxs-lookup"><span data-stu-id="91dfc-114">On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.</span></span>
4. <span data-ttu-id="91dfc-115">Click the **Configure** tab.</span><span class="sxs-lookup"><span data-stu-id="91dfc-115">Click the **Configure** tab.</span></span>

    ![Virtual networks window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. <span data-ttu-id="91dfc-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span><span class="sxs-lookup"><span data-stu-id="91dfc-117">In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.</span></span>
6. <span data-ttu-id="91dfc-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91dfc-118">To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.</span></span>

   ![Update the DNS server settings for the virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
> <span data-ttu-id="91dfc-120">After you update the DNS server settings for the virtual network, it might take a while for the virtual machines on the network to get the updated DNS configuration.</span><span class="sxs-lookup"><span data-stu-id="91dfc-120">After you update the DNS server settings for the virtual network, it might take a while for the virtual machines on the network to get the updated DNS configuration.</span></span> <span data-ttu-id="91dfc-121">If a virtual machine is unable to connect to the domain, you can flush the DNS cache ('ipconfig /flushdns') on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="91dfc-121">If a virtual machine is unable to connect to the domain, you can flush the DNS cache ('ipconfig /flushdns') on the virtual machine.</span></span> <span data-ttu-id="91dfc-122">This command forces a refresh of the DNS settings on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="91dfc-122">This command forces a refresh of the DNS settings on the virtual machine.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="91dfc-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="91dfc-123">Next steps</span></span>
<span data-ttu-id="91dfc-124">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="91dfc-124">Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)</span></span>



