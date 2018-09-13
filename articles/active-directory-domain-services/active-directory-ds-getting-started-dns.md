---
title: 'Azure Active Directory Domain Services: Update DNS settings for the Azure virtual network | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/30/2018
ms.author: maheshu
ms.openlocfilehash: f683eeee05f264ca239b8f1da2bc5078e0146a17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827125"
---
# <a name="enable-azure-active-directory-domain-services"></a>Enable Azure Active Directory Domain Services

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a>Task 4: update DNS settings for the Azure virtual network
In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory. Next, enable computers within the virtual network to connect and consume these services. In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.

To update the DNS server settings for the virtual network in which you have enabled Azure Active Directory Domain Services, complete the following steps:


1. The **Overview** tab lists a set of **Required configuration steps** to be performed after your managed domain is fully provisioned. The first configuration step is **Update DNS server settings for your virtual network**.

    ![Domain Services - Overview tab](./media/getting-started/domain-services-provisioned-overview.png)

    > [!TIP]
    > Dont see this configuration step? If the DNS server settings for your virtual network are up to date, you will not see the 'Update DNS server settings for your virtual network' tile on the Overview tab.
    >
    >

2. Click the **Configure** button to update the DNS server settings for the virtual network.

> [!NOTE]
> Virtual machines in the network only get the new DNS settings after a restart. If you need them to get the updated DNS settings right away, trigger a restart either by the portal, PowerShell, or the CLI.
>
>

## <a name="next-step"></a>Next step
[Task 5: enable password hash synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)
