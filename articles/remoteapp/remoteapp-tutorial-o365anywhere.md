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
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get the same Office 365 experience on any device with Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

This article will cover how to deploy Office 365 on any device in your company. Your users can get the same capabilities and UI experience on Android, Apple and Windows.

We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to. This set of virtual machines we call a "cloud collection".

## <a name="create-a-cloud-collection"></a>Create a cloud collection
First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.
![Showing Azure RemoteApp on the Azure Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/1-menu.png)

Then continue by clicking **new** on the bottom and "quick creating" a collection. Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.
![Create Dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Once you finish the form the collection creation process should start. This may take up to an hour or so.

![Waiting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Once the process is done, it will look something like this. If we click **Publishing** we can see that most Office applications have been published for us already.
![Collection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/4-done.png)

![Published apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/5-publish.png)

At this point you can also add more users that have access to this collection by clicking **User Access**.
![Configure user access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/6-user.png)

Now let's try out connecting to Office 365!

## <a name="connect-to-office-365"></a>Connect to Office 365
We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on. The screenshots below are for Windows.

Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now. When you're signed in you should see a notification about new invitations, click there and you should see a list like one below. Accept the invitation that matches your Azure account owner email.

![New invitation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/7-araclient.png)

What it looks like when there are new invitations.

![Accept an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.

![List of apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/9-work.png)

When you click on any of these the application should start on the Azure virtual machine and you should be all set! Enjoy!

![starting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-tutorial-o365anywhere/11-pp.png)












