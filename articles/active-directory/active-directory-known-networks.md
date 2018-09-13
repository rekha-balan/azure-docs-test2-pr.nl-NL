---
title: Known Networks in the Azure classic portal | Microsoft Docs
description: By configuring known networks, you can avoid having IP addresses that are owned by your organization included in the Sign ins from multiple geographies and Sign ins from IP addresses with suspicious activity reports.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 127e730726788523e4de1c67305fcfeb01e82d89
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554489"
---
# <a name="known-networks"></a><span data-ttu-id="1675b-103">Known networks</span><span class="sxs-lookup"><span data-stu-id="1675b-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [Azure classic portal](active-directory-known-networks.md)
> * [Azure portal](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="1675b-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span><span class="sxs-lookup"><span data-stu-id="1675b-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="1675b-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span><span class="sxs-lookup"><span data-stu-id="1675b-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="1675b-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span><span class="sxs-lookup"><span data-stu-id="1675b-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="1675b-109">This can, for example, happen when:</span><span class="sxs-lookup"><span data-stu-id="1675b-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="1675b-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span><span class="sxs-lookup"><span data-stu-id="1675b-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="1675b-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span><span class="sxs-lookup"><span data-stu-id="1675b-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="1675b-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span><span class="sxs-lookup"><span data-stu-id="1675b-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="1675b-113">To add your organization’s public IP address ranges, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1675b-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="1675b-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1675b-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="1675b-115">In the left pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1675b-115">In the left pane, click **Active Directory**.</span></span> 

    ![Known networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="1675b-117">In the **Directory** tab, select your directory.</span><span class="sxs-lookup"><span data-stu-id="1675b-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="1675b-118">In the menu on the top, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="1675b-118">In the menu on the top, click **Configure**.</span></span> 

    ![Known networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="1675b-120">On the Configure tab, go to **your organizations public IP address ranges**</span><span class="sxs-lookup"><span data-stu-id="1675b-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![Known networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="1675b-122">Click **Add Known IP Address Ranges**.</span><span class="sxs-lookup"><span data-stu-id="1675b-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="1675b-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span><span class="sxs-lookup"><span data-stu-id="1675b-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![Known networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="1675b-125">**Additional resources:**</span><span class="sxs-lookup"><span data-stu-id="1675b-125">**Additional resources:**</span></span>

* [<span data-ttu-id="1675b-126">View your access and usage reports</span><span class="sxs-lookup"><span data-stu-id="1675b-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="1675b-127">Sign ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="1675b-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="1675b-128">Sign ins from multiple geographies</span><span class="sxs-lookup"><span data-stu-id="1675b-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)





