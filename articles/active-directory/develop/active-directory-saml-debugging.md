---
title: How to debug SAML-based single sign-on to applications in Azure Active Directory | Microsoft Docs
description: 'Learn how to debug SAML-based single sign-on to applications in Azure Active Directory '
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: asmalser
ms.openlocfilehash: e6b00aeb2438353c7b2b63260e170336c0386b52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563249"
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="07963-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07963-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="07963-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span><span class="sxs-lookup"><span data-stu-id="07963-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="07963-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span><span class="sxs-lookup"><span data-stu-id="07963-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="07963-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span><span class="sxs-lookup"><span data-stu-id="07963-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="07963-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span><span class="sxs-lookup"><span data-stu-id="07963-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="07963-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span><span class="sxs-lookup"><span data-stu-id="07963-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="07963-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span><span class="sxs-lookup"><span data-stu-id="07963-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="07963-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span><span class="sxs-lookup"><span data-stu-id="07963-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="07963-111">Related Articles</span><span class="sxs-lookup"><span data-stu-id="07963-111">Related Articles</span></span>
* [<span data-ttu-id="07963-112">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07963-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="07963-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="07963-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="07963-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span><span class="sxs-lookup"><span data-stu-id="07963-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saml-debugging/fiddler.png
