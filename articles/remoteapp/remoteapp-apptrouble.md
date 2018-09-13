---
title: Azure RemoteApp Troubleshooting - Application launch and connection failures  | Microsoft Docs
description: Learn how to troubleshoot issues with starting and connecting to applications in Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cdf0a2133bd50048fb441d49c62cb1508858f31c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564685"
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Troubleshoot Azure RemoteApp - Application launch and connection failures
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

Applications hosted in Azure RemoteApp can fail to launch for a few different reasons. This article describes various reasons and error messages users might receive when trying to launch applications. It also talks about connection failures. (But this article does not describe issues when signing into the Azure RemoteApp client.)  

Read on for information about common error messages due to app launch and connection failures.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>We're getting you set up... Try again in 10 minutes.
This error means Azure RemoteApp is scaling up to meet the capacity need of your users. In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users. Typically this takes around five minutes but can take up to 10 minutes. Sometimes, this doesn't happen fast enough and resources are needed immediately. For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time. If this happens to you we can enable **capacity mode** on the back end. To do this open an Azure Support ticket. Be certain to include your subscription ID in the request.  

![We are getting you set up](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a>Could not auto-reconnect to your applications, please re-launch your application
This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.  Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.

![Could not auto-reconnect to your applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a>Problems with the temp profile
This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.  Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user. This will force a full log off of the user session - then have the user attempt to launch an app again. If that fails contact Azure support.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp has stopped working
This error message means the Azure RemoteApp client is having an issue and needs to be restarted. Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.  If the issue continues open and Azure Support ticket.

![Azure RemoteApp has stopped working](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a>An error occurred while Remote Desktop Connection was accessing this resource. Retry the connection or contact your system administrator
This is a generic error message - contact Azure support so we can investigate. 

![Generic Azure RemoteApp message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble4.png) 





