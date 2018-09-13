---
title: Azure RemoteApp best practices | Microsoft Docs
description: Best practices for configuring and using Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: fda356fc5fd6e9888138a06a0b72232e3581567b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555257"
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Best practices for configuring and using Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.
> 
> 

The following information can help you configure and use Azure RemoteApp productively.

## <a name="connectivity"></a>Connectivity
* Always use the latest client version. Using older clients might result in connectivity issues and other degraded experiences. Enabling automatic application updates for your device will ensure that the latest client is always installed.
* Always use the most stable and reliable internet connection available to you.  
* Use only supported proxy connections for optimal connectivity performance.  The SOCKS proxy is not supported.

## <a name="applications"></a>Applications
* Save and close RemoteApp applications when you are done with the application. Not closing the application might result in data loss.
* Validate custom applications before using them in Azure RemoteApp. This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection. For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configuration and management
* Keep your template images up to date, installing software updates and other critical fixes as needed. This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.  
* Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable. Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.
* Configure template images with installed applications, roles, or features such that they are stateless. They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.
  * Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.
  * Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.
  * Configure any system-wide settings in the template image rather than on individual virtual machines in a service.
  * Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.

