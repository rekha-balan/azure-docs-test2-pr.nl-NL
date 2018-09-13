---
title: Managing custom domain names in your Azure Active Directory preview | Microsoft Docs
description: Management concepts and how-tos for managing a domain name in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: curtand;jeffsta
ms.openlocfilehash: 75b357ef4674ac7c36f6c21ea18dc6e462efaabf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548941"
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory-preview"></a>Managing custom domain names in your Azure Active Directory preview
A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application. A resource in Azure Active Directory (Azure AD) preview can include a domain name that is already verified to be owned by the directory that contains the resource. [What's in the preview?](active-directory-preview-explainer.md) Only a global administrator can perform domain management tasks in Azure AD.

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a>Set the primary domain name for your Azure AD directory
When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name. The primary domain is the default domain name for a new user when you create a new user. This streamlines the process for an administrator to create new users in the portal. To change the primary domain name:

1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.
   
   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-domains-add-azure-portal/user-management.png)
3. On the ***directory-name*** blade, select **Domain names**.
4. On the ***directory-name* - Domain names** blade, select the domain name you would like to make the primary domain name.
5. On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), select the **Make primary** command. Confirm your choice when prompted.
   
   ![Make a domain name primary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-domains-manage-azure-portal/make-primary.png)

You can change the primary domain name for your directory to be any verified custom domain that is not federated. Changing the primary domain for your directory will not change the user names for any existing users.

## <a name="add-custom-domain-names-to-your-azure-ad"></a>Add custom domain names to your Azure AD
You can add up to 900 custom domain names to each Azure AD directory. The process to [add an additional custom domain name](active-directory-domains-add-azure-portal.md) is the same for the first custom domain name.

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
Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API (in public preview).

* [Using PowerShell to manage domain names in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Using Graph API to manage domain names in Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Next steps
* [Add custom domain names](active-directory-domains-add-azure-portal.md)



