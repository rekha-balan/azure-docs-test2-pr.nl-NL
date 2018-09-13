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
# <a name="update-dns-settings-for-the-azure-virtual-network"></a>Update DNS settings for the Azure virtual network
## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a>Task 4: Update DNS settings for the Azure virtual network
In the preceding configuration tasks, you have successfully enabled Azure Active Directory Domain Services for your directory. The next task is to ensure that computers within the virtual network can connect and consume these services. In this article, you update the DNS server settings for your virtual network to point to the two IP addresses where Azure Active Directory Domain Services is available on the virtual network.

> [!NOTE]
> After you've enabled Azure Active Directory Domain Services for the directory, note the IP addresses for Azure Active Directory Domain Services that are displayed on the **Configure** tab of your directory.
>
>

To update the DNS server setting for the virtual network in which you have enabled Azure Active Directory Domain Services, do the following:

1. Go to the [Azure classic portal](https://manage.windowsazure.com).
2. In the left pane, select **Networks**.  
    The **Networks** window opens.

    ![Virtual networks window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. On the **Virtual Networks** tab, select the virtual network in which you enabled Azure Active Directory Domain Services to view its properties.
4. Click the **Configure** tab.

    ![Virtual networks window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. In the **DNS servers** section, enter both of the IP addresses that were displayed in the **Domain Services** section on the **Configure** tab of your directory.
6. To save the DNS server settings for this virtual network, in the task pane at the bottom of the window, click **Save**.

   ![Update the DNS server settings for the virtual network](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
> After you update the DNS server settings for the virtual network, it might take a while for the virtual machines on the network to get the updated DNS configuration. If a virtual machine is unable to connect to the domain, you can flush the DNS cache ('ipconfig /flushdns') on the virtual machine. This command forces a refresh of the DNS settings on the virtual machine.
>
>

## <a name="next-steps"></a>Next steps
Task 5: [Enable password synchronization to Azure Active Directory Domain Services](active-directory-ds-getting-started-password-sync.md)



