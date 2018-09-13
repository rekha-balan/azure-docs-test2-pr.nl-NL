---
title: Using Outlook in Azure RemoteApp | Microsoft Docs
description: Learn how to configure and use Outlook in Azure RemoteApp | Microsoft Azure
services: remoteapp
documentationcenter: ''
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a6d4fbdf0e552f50673092183e893841ec0c5aa4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549956"
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a><span data-ttu-id="715e7-103">Using Microsoft Outlook in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="715e7-103">Using Microsoft Outlook in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="715e7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="715e7-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="715e7-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="715e7-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="715e7-106">Azure RemoteApp supports Microsoft Outlook O365.</span><span class="sxs-lookup"><span data-stu-id="715e7-106">Azure RemoteApp supports Microsoft Outlook O365.</span></span> <span data-ttu-id="715e7-107">Read more about how [Office works in Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="715e7-107">Read more about how [Office works in Azure RemoteApp](remoteapp-officesubscription.md).</span></span> <span data-ttu-id="715e7-108">There are a few recommended settings for Outlook when used in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="715e7-108">There are a few recommended settings for Outlook when used in Azure RemoteApp.</span></span>

## <a name="cached-mode"></a><span data-ttu-id="715e7-109">Cached mode</span><span class="sxs-lookup"><span data-stu-id="715e7-109">Cached mode</span></span>
<span data-ttu-id="715e7-110">Cached mode is a recommended configuration when using Outlook in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="715e7-110">Cached mode is a recommended configuration when using Outlook in Azure RemoteApp.</span></span> <span data-ttu-id="715e7-111">When you configure an Outlook 2013 account to use Cached Exchange Mode, Outlook 2013 works from a local copy of the user's Microsoft Exchange mailbox that is stored in an offline data file (OST file) on the user's computer, together with the Offline Address Book (OAB).</span><span class="sxs-lookup"><span data-stu-id="715e7-111">When you configure an Outlook 2013 account to use Cached Exchange Mode, Outlook 2013 works from a local copy of the user's Microsoft Exchange mailbox that is stored in an offline data file (OST file) on the user's computer, together with the Offline Address Book (OAB).</span></span> <span data-ttu-id="715e7-112">The cached mailbox and OAB are updated periodically from the O365 service.</span><span class="sxs-lookup"><span data-stu-id="715e7-112">The cached mailbox and OAB are updated periodically from the O365 service.</span></span> <span data-ttu-id="715e7-113">Read more about [the differences between cached and online mode](https://technet.microsoft.com/library/jj683103.aspx).</span><span class="sxs-lookup"><span data-stu-id="715e7-113">Read more about [the differences between cached and online mode](https://technet.microsoft.com/library/jj683103.aspx).</span></span>

<span data-ttu-id="715e7-114">The user can select **Cached Exchange Mode** or **Online Mode** during account setup or by changing the account settings.</span><span class="sxs-lookup"><span data-stu-id="715e7-114">The user can select **Cached Exchange Mode** or **Online Mode** during account setup or by changing the account settings.</span></span> <span data-ttu-id="715e7-115">You can also deploy one mode or the other by using the Office Customization Tool (OCT) or Group Policy.</span><span class="sxs-lookup"><span data-stu-id="715e7-115">You can also deploy one mode or the other by using the Office Customization Tool (OCT) or Group Policy.</span></span>  

<span data-ttu-id="715e7-116">Read [step by step instructions on enabling cached mode](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).</span><span class="sxs-lookup"><span data-stu-id="715e7-116">Read [step by step instructions on enabling cached mode](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).</span></span>

## <a name="search"></a><span data-ttu-id="715e7-117">Search</span><span class="sxs-lookup"><span data-stu-id="715e7-117">Search</span></span>
<span data-ttu-id="715e7-118">In Azure RemoteApp, using search within Outlook has limitations.</span><span class="sxs-lookup"><span data-stu-id="715e7-118">In Azure RemoteApp, using search within Outlook has limitations.</span></span> <span data-ttu-id="715e7-119">Azure RemoteApp uses pooled VMs to accommodate user sessions.</span><span class="sxs-lookup"><span data-stu-id="715e7-119">Azure RemoteApp uses pooled VMs to accommodate user sessions.</span></span> <span data-ttu-id="715e7-120">Search indexing depends on the machine ID, which is different for different VMs.</span><span class="sxs-lookup"><span data-stu-id="715e7-120">Search indexing depends on the machine ID, which is different for different VMs.</span></span> <span data-ttu-id="715e7-121">It is possible that every time a user logs into Azure RemoteApp, they are directed to a new VM.</span><span class="sxs-lookup"><span data-stu-id="715e7-121">It is possible that every time a user logs into Azure RemoteApp, they are directed to a new VM.</span></span> <span data-ttu-id="715e7-122">That would mean, if we enable local search, the indexer will run every time the machine ID changes (when the user is on a different VM).</span><span class="sxs-lookup"><span data-stu-id="715e7-122">That would mean, if we enable local search, the indexer will run every time the machine ID changes (when the user is on a different VM).</span></span> <span data-ttu-id="715e7-123">Depending on the size of the .OST file, the indexer could take a long time to complete and use up resources needed for other apps.</span><span class="sxs-lookup"><span data-stu-id="715e7-123">Depending on the size of the .OST file, the indexer could take a long time to complete and use up resources needed for other apps.</span></span> <span data-ttu-id="715e7-124">Search would not only be slow but might not produce results.</span><span class="sxs-lookup"><span data-stu-id="715e7-124">Search would not only be slow but might not produce results.</span></span> <span data-ttu-id="715e7-125">Using an Online Mode account profile would work around this, but overall performance would suffer due to the lack of a local cache (see the link above for more information about the difference between cached and online mode).</span><span class="sxs-lookup"><span data-stu-id="715e7-125">Using an Online Mode account profile would work around this, but overall performance would suffer due to the lack of a local cache (see the link above for more information about the difference between cached and online mode).</span></span> <span data-ttu-id="715e7-126">Unfortunately, indexed/local search cannot be disabled and online search cannot be enabled by default in Outlook 2013.</span><span class="sxs-lookup"><span data-stu-id="715e7-126">Unfortunately, indexed/local search cannot be disabled and online search cannot be enabled by default in Outlook 2013.</span></span>

