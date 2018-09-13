---
title: What is in the Azure RemoteApp template images? | Microsoft Docs
description: Learn about the template images included with Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 348306795fd3c8275b21e4ec6dceae408916bf72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564082"
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a>What is in the Azure RemoteApp template images?
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

Your Azure RemoteApp subscription includes three template images:

* Windows Server 2012
* Microsoft Office 365 ProPlus (Office 365 subscription required)
* Microsoft Office 2013 Professional Plus (trial only)

> [!IMPORTANT]
> Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production. This means that you can share the programs or apps on the template images with your users. For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.
> 
> Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information. And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.
> 
> 

Read on for details on what each image contains.

## <a name="windows-server-2012-r2--the-vanilla-image"></a>Windows Server 2012 R2  ("the vanilla image")
This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:

* .NET Framework 4.5, 3.5.1, 3.5
* Desktop Experience
* Ink and Handwriting Services
* Media Foundation
* Remote Desktop Session Host
* Windows PowerShell 4.0
* Windows PowerShell ISE
* WoW64 Support

This image also has the following applications installed:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (subscription required)
Office 365 is the most requested application, so we created a "custom" image for you to work with.

This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:

* Access
* Excel
* Lync
* OneNote
* OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Microsoft Office Proofing Tools

The image also includes Visio Pro and Project Pro.

And the following applications, as well:

* SQL Native client
* ODBC Driver
* SQL Server Data Mining client
* MasterDataServices client
* Microsoft Publisher
* PowerQuery
* PowerMap

Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan. For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx). Still have questions? Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information. Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).

Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (trial only)
During the free trial period, you can test the service with the Office 2013 image.

This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:

* Access
* Excel
* Lync
* OneNote
* OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Microsoft Office Proofing Tools

> [!IMPORTANT]
> **Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*. The Office 2013 Professional Plus image is intended for trial use only. If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image. For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)
> 
> 

