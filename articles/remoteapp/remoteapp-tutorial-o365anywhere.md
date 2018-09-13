---
title: Get the same Office 365 experience on any device with Azure RemoteApp | Microsoft Docs
description: Learn how to share any Office 365 app with your users by using Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: guscatalano
manager: mbaldwin
editor: ''
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 90c08dabb0c84601c1f54fb84e3dac11296aef16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550492"
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="22b05-103">Get the same Office 365 experience on any device with Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="22b05-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22b05-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="22b05-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="22b05-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="22b05-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="22b05-106">This article will cover how to deploy Office 365 on any device in your company.</span><span class="sxs-lookup"><span data-stu-id="22b05-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="22b05-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span><span class="sxs-lookup"><span data-stu-id="22b05-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="22b05-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span><span class="sxs-lookup"><span data-stu-id="22b05-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="22b05-109">This set of virtual machines we call a "cloud collection".</span><span class="sxs-lookup"><span data-stu-id="22b05-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="22b05-110">Create a cloud collection</span><span class="sxs-lookup"><span data-stu-id="22b05-110">Create a cloud collection</span></span>
<span data-ttu-id="22b05-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span><span class="sxs-lookup"><span data-stu-id="22b05-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="22b05-112">![Showing Azure RemoteApp on the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="22b05-112">![Showing Azure RemoteApp on the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="22b05-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span><span class="sxs-lookup"><span data-stu-id="22b05-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="22b05-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span><span class="sxs-lookup"><span data-stu-id="22b05-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="22b05-115">![Create Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="22b05-115">![Create Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="22b05-116">Once you finish the form the collection creation process should start.</span><span class="sxs-lookup"><span data-stu-id="22b05-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="22b05-117">This may take up to an hour or so.</span><span class="sxs-lookup"><span data-stu-id="22b05-117">This may take up to an hour or so.</span></span>

![Waiting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="22b05-119">Once the process is done, it will look something like this.</span><span class="sxs-lookup"><span data-stu-id="22b05-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="22b05-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span><span class="sxs-lookup"><span data-stu-id="22b05-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="22b05-121">![Collection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="22b05-121">![Collection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Published apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="22b05-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span><span class="sxs-lookup"><span data-stu-id="22b05-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="22b05-124">![Configure user access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="22b05-124">![Configure user access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="22b05-125">Now let's try out connecting to Office 365!</span><span class="sxs-lookup"><span data-stu-id="22b05-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="22b05-126">Connect to Office 365</span><span class="sxs-lookup"><span data-stu-id="22b05-126">Connect to Office 365</span></span>
<span data-ttu-id="22b05-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span><span class="sxs-lookup"><span data-stu-id="22b05-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="22b05-128">The screenshots below are for Windows.</span><span class="sxs-lookup"><span data-stu-id="22b05-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="22b05-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span><span class="sxs-lookup"><span data-stu-id="22b05-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="22b05-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span><span class="sxs-lookup"><span data-stu-id="22b05-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="22b05-131">Accept the invitation that matches your Azure account owner email.</span><span class="sxs-lookup"><span data-stu-id="22b05-131">Accept the invitation that matches your Azure account owner email.</span></span>

![New invitation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="22b05-133">What it looks like when there are new invitations.</span><span class="sxs-lookup"><span data-stu-id="22b05-133">What it looks like when there are new invitations.</span></span>

![Accept an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="22b05-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span><span class="sxs-lookup"><span data-stu-id="22b05-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![List of apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="22b05-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span><span class="sxs-lookup"><span data-stu-id="22b05-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="22b05-138">Enjoy!</span><span class="sxs-lookup"><span data-stu-id="22b05-138">Enjoy!</span></span>

![starting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/11-pp.png)












