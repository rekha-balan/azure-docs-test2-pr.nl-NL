---
title: 'Azure Active Directory B2C: Custom attributes | Microsoft Docs'
description: How to use custom attributes in Azure Active Directory B2C to collect information about your consumers
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: f7b21cc941f17d0815316dfe7013e9f97a95c223
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555242"
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a>Azure Active Directory B2C: Use custom attributes to collect information about your consumers
Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes. However, every consumer-facing application has unique requirements on what attributes to gather from consumers. With Azure AD B2C, you can extend the set of attributes stored on each consumer account. You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below. You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Create a custom attribute
1. [Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).
2. Click **User attributes**.
3. Click **+Add** at the top of the blade.
4. Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**. Click **Create**.
   
   > [!NOTE]
   > Only the "String" **Data Type** is currently available.
   > 
   > 

The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Use a custom attribute in your sign-up policy
1. [Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).
2. Click **Sign-up policies**.
3. Click your sign-up policy (for example, "B2C_1_SiUp") to open it. Click **Edit** at the top of the blade.
4. Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize"). Click **OK**.
5. Click **Application claims** and select the custom attribute. Click **OK**.
6. Click **Save** at the top of the blade.

You can use the "Run now" feature on the policy to verify the consumer experience. You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.

## <a name="notes"></a>Notes
* Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.
* There is a known limitation of custom attributes. It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.

