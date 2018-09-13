---
title: Managing custom domain names in your Azure Active Directory | Microsoft Docs
description: Management concepts and how-tos for managing a domain name in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 11/14/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.openlocfilehash: b503ef4c5cd922d4f7b58940cfc98a83a78ae986
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864883"
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Managing custom domain names in your Azure Active Directory
A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application. A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by the directory that contains the resource. Only a global administrator can perform domain management tasks in Azure AD.

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a>Set the primary domain name for your Azure AD directory
When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name. The primary domain is the default domain name for a new user when you create a new user. Setting a primary domain name streamlines the process for an administrator to create new users in the portal. To change the primary domain name:

1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **Azure Active Directory**.
3. Select **Custom domain names**.
     
   ![Opening user management](./media/domains-manage/add-custom-domain.png)
4. Select the name of the domain that you want to be the primary domain.
5. Select the **Make primary** command. Confirm your choice when prompted.
   
   ![Make a domain name primary](./media/domains-manage/make-primary-domain.png)

You can change the primary domain name for your directory to be any verified custom domain that is not federated. Changing the primary domain for your directory will not change the user names for any existing users.

## <a name="add-custom-domain-names-to-your-azure-ad-tenant"></a>Add custom domain names to your Azure AD tenant
You can add up to a maximum of 900 managed domain names. If you are configuring all your domains for federation with on-premises Active Directory, you can add up to a maximum of 450 domain names in each directory. For more information, see [Federated and managed domain names](https://docs.microsoft.com/azure/active-directory/active-directory-add-domain-concepts#federated-and-managed-domain-names).

## <a name="add-subdomains-of-a-custom-domain"></a>Add subdomains of a custom domain
If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com. The subdomain will be automatically verified by Azure AD. To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a>What to do if you change the DNS registrar for your custom domain name
If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks. If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.

## <a name="delete-a-custom-domain-name"></a>Delete a custom domain name
You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.

To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name. You can't delete a domain name from your directory if:

* Any user has a user name, email address, or proxy address that includes the domain name.
* Any group has an email address or proxy address that includes the domain name.
* Any application in your Azure AD has an app ID URI that includes the domain name.

You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a>Use PowerShell or Graph API to manage domain names
Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.

* [Using PowerShell to manage domain names in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Using Graph API to manage domain names in Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Next steps
* [Add custom domain names](../fundamentals/add-custom-domain.md)

