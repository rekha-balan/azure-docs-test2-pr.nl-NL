---
title: 'Azure Active Directory Domain Services: Create the Azure AD DC administrators group | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: maheshu
ms.openlocfilehash: bde4a5a215cc072ea014c030c22e5910014d0f72
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551628"
---
# <a name="get-started-with-azure-active-directory-domain-services"></a>Get started with Azure Active Directory Domain Services
This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a>Task 1: Create the Azure AD DC administrators group
The first task is to create an administrative group in your Azure AD tenant. This special administrative group is called *AAD DC Administrators*. Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain. On domain-joined machines, this group is added to the administrators group. Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.  

> [!NOTE]
> You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services. On managed domains, these permissions are reserved by the service and are not made available to users within the tenant. However, you can use the special administrative group created in this configuration task to perform some privileged operations. These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.
>

In this configuration task, you create the administrative group and add one or more users in your directory to the group. To create the administrative group for Azure Active Directory Domain Services, do the following:

1. Go to the [Azure classic portal](https://manage.windowsazure.com).
2. In the left pane, select the **Active Directory** button.
3. Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services. You can create only one domain for each Azure AD directory.

    ![Select Azure AD directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. On the **preview directory** page, click the **Groups** tab.
5. To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.

    ![The Add Group button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/add-group-button.png)
6. In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.

   > [!WARNING]
   > To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.
   >
   >

    ![The Add Group dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/create-admin-group.png)
7. In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.
8. After you've created the group, click the group name to view its properties. 
9. To add users as members of the group, at the bottom of the window, click the **Add Members** button.

    ![Add group members button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.

    ![Add users to administrators group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/add-group-members.png)

## <a name="next-steps"></a>Next steps
Task 2: [Create or select an Azure virtual network](active-directory-ds-getting-started-vnet.md)
  





