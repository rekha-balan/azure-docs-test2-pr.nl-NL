---
title: Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory | Microsoft Docs
description: Learn how to custom the claims issued in the SAML token for pre-integrated apps in Azure Active Directory
services: active-directory
documentationcenter: ''
author: asmalser-msft
manager: femila
editor: ''
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: asmalser
ms.openlocfilehash: 8eade12ae91f7c7570b8a5694351c20f9505cd35
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662215"
---
# <a name="customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a><span data-ttu-id="50f68-103">Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50f68-103">Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory</span></span>
<span data-ttu-id="50f68-104">Today Azure Active Directory supports thousands of pre-integrated applications in the Azure AD Application Gallery, including over 150 that support single sign-on using the SAML 2.0 protocol.</span><span class="sxs-lookup"><span data-stu-id="50f68-104">Today Azure Active Directory supports thousands of pre-integrated applications in the Azure AD Application Gallery, including over 150 that support single sign-on using the SAML 2.0 protocol.</span></span> <span data-ttu-id="50f68-105">When a user authenticates to an application through Azure AD using SAML, Azure AD sends a token to the application (via an HTTP 302 redirect) which the application then validates and uses to log the user in instead of prompting for a username and password.</span><span class="sxs-lookup"><span data-stu-id="50f68-105">When a user authenticates to an application through Azure AD using SAML, Azure AD sends a token to the application (via an HTTP 302 redirect) which the application then validates and uses to log the user in instead of prompting for a username and password.</span></span> <span data-ttu-id="50f68-106">These SAML tokens contains pieces of information about the user known as "claims".</span><span class="sxs-lookup"><span data-stu-id="50f68-106">These SAML tokens contains pieces of information about the user known as "claims".</span></span>

<span data-ttu-id="50f68-107">In identity-speak, a �claim� is information that an identity provider states about a user inside the token they issue for that user.</span><span class="sxs-lookup"><span data-stu-id="50f68-107">In identity-speak, a �claim� is information that an identity provider states about a user inside the token they issue for that user.</span></span> <span data-ttu-id="50f68-108">In a [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), this data is typically contained in the SAML Attribute Statement, and the user�s unique ID is typically represented in the SAML Subject.</span><span class="sxs-lookup"><span data-stu-id="50f68-108">In a [SAML token](http://en.wikipedia.org/wiki/SAML_2.0), this data is typically contained in the SAML Attribute Statement, and the user�s unique ID is typically represented in the SAML Subject.</span></span>

<span data-ttu-id="50f68-109">By default, Azure AD will issue a SAML token to your application that contains a NameIdentifier claim, with a value of the user�s username in Azure AD (this value uniquely identifies the user).</span><span class="sxs-lookup"><span data-stu-id="50f68-109">By default, Azure AD will issue a SAML token to your application that contains a NameIdentifier claim, with a value of the user�s username in Azure AD (this value uniquely identifies the user).</span></span> <span data-ttu-id="50f68-110">The SAML token also contains additional claims containing the user�s email address, first name, and last name.</span><span class="sxs-lookup"><span data-stu-id="50f68-110">The SAML token also contains additional claims containing the user�s email address, first name, and last name.</span></span>

<span data-ttu-id="50f68-111">To view or edit the claims issued in the SAML token to the application, open the application record in the Azure management portal and select the **Attributes** tab underneath the application.</span><span class="sxs-lookup"><span data-stu-id="50f68-111">To view or edit the claims issued in the SAML token to the application, open the application record in the Azure management portal and select the **Attributes** tab underneath the application.</span></span>

![][1]

<span data-ttu-id="50f68-112">There are two possible reasons why you might need to edit the claims issued in the SAML token: �The application has been written to require a different set of claim URIs or claim values �Your application has been deployed in a way that requires the NameIdentifier claim to be something other than the username (AKA user principal name) stored in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50f68-112">There are two possible reasons why you might need to edit the claims issued in the SAML token: �The application has been written to require a different set of claim URIs or claim values �Your application has been deployed in a way that requires the NameIdentifier claim to be something other than the username (AKA user principal name) stored in Azure Active Directory.</span></span> 

<span data-ttu-id="50f68-113">You can edit any of the default claim values by selecting the pencil-shaped icon that appears on the right whenever you mouse over one of the rows in the SAML token attributes table.</span><span class="sxs-lookup"><span data-stu-id="50f68-113">You can edit any of the default claim values by selecting the pencil-shaped icon that appears on the right whenever you mouse over one of the rows in the SAML token attributes table.</span></span> <span data-ttu-id="50f68-114">You can also remove claims (other than NameIdentifier) using the **X** icon, and add new claims using the **Add user attribute** button.</span><span class="sxs-lookup"><span data-stu-id="50f68-114">You can also remove claims (other than NameIdentifier) using the **X** icon, and add new claims using the **Add user attribute** button.</span></span>

## <a name="editing-the-nameidentifier-claim"></a><span data-ttu-id="50f68-115">Editing the NameIdentifier claim</span><span class="sxs-lookup"><span data-stu-id="50f68-115">Editing the NameIdentifier claim</span></span>
<span data-ttu-id="50f68-116">To solve the problem where the application has been deployed using a different username, click the pencil icon next to the NameIdentifier claim.</span><span class="sxs-lookup"><span data-stu-id="50f68-116">To solve the problem where the application has been deployed using a different username, click the pencil icon next to the NameIdentifier claim.</span></span> <span data-ttu-id="50f68-117">This provides a dialog with several different options:</span><span class="sxs-lookup"><span data-stu-id="50f68-117">This provides a dialog with several different options:</span></span>

![][2]

<span data-ttu-id="50f68-118">In the **Attribute Value** menu, select **user.mail** to set the NameIdentifier claim to be the user�s email address in the directory, or select **user.onpremisessamaccountname** to set to the user�s SAM Account Name that has been synced from on-premise Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50f68-118">In the **Attribute Value** menu, select **user.mail** to set the NameIdentifier claim to be the user�s email address in the directory, or select **user.onpremisessamaccountname** to set to the user�s SAM Account Name that has been synced from on-premise Azure AD.</span></span> 

<span data-ttu-id="50f68-119">You can also use the special ExtractMailPrefix() function to remove the domain suffix from either the email address or the user principal name resulting in only the first part of the user name being passed through (e.g. �joesmith� instead of joesmith@contoso.com).</span><span class="sxs-lookup"><span data-stu-id="50f68-119">You can also use the special ExtractMailPrefix() function to remove the domain suffix from either the email address or the user principal name resulting in only the first part of the user name being passed through (e.g. �joesmith� instead of joesmith@contoso.com).</span></span>

![][3]

## <a name="adding-claims"></a><span data-ttu-id="50f68-120">Adding claims</span><span class="sxs-lookup"><span data-stu-id="50f68-120">Adding claims</span></span>
<span data-ttu-id="50f68-121">When adding a new claim, you can specify the attribute name (which doesn�t strictly need to follow a URI pattern as per the SAML spec), as well as set the value to any user attribute that is stored in the directory.</span><span class="sxs-lookup"><span data-stu-id="50f68-121">When adding a new claim, you can specify the attribute name (which doesn�t strictly need to follow a URI pattern as per the SAML spec), as well as set the value to any user attribute that is stored in the directory.</span></span>

![][4]

<span data-ttu-id="50f68-122">For example, if you need to send the department that the user belongs to in their organization as a claim (e.g. Sales), then you can enter whatever claim value is expected by the application, and then select **user.department** as the value.</span><span class="sxs-lookup"><span data-stu-id="50f68-122">For example, if you need to send the department that the user belongs to in their organization as a claim (e.g. Sales), then you can enter whatever claim value is expected by the application, and then select **user.department** as the value.</span></span>

<span data-ttu-id="50f68-123">If for a given user there is no value stored for a selected attribute, then that claim with not be issued in the token.</span><span class="sxs-lookup"><span data-stu-id="50f68-123">If for a given user there is no value stored for a selected attribute, then that claim with not be issued in the token.</span></span>

<span data-ttu-id="50f68-124">**Note:** The **user.onpremisesecurityidentifier** and **user.onpremisesamaccountname** are only supported when synchronizing user data from on-premise Active Directory using the [Azure AD Connect tool](../active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="50f68-124">**Note:** The **user.onpremisesecurityidentifier** and **user.onpremisesamaccountname** are only supported when synchronizing user data from on-premise Active Directory using the [Azure AD Connect tool](../active-directory-aadconnect.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="50f68-125">Related Articles</span><span class="sxs-lookup"><span data-stu-id="50f68-125">Related Articles</span></span>
* [<span data-ttu-id="50f68-126">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50f68-126">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="50f68-127">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="50f68-127">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="50f68-128">Troubleshooting SAML-Based Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="50f68-128">Troubleshooting SAML-Based Single Sign-On</span></span>](active-directory-saml-debugging.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saml-claims-customization/claimscustomization1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saml-claims-customization/claimscustomization2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saml-claims-customization/claimscustomization3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saml-claims-customization/claimscustomization4.png



