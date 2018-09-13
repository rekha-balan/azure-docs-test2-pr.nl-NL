---
title: 'Azure AD Connect sync: Directory extensions | Microsoft Docs'
description: This topic describes the directory extensions feature in Azure AD Connect.
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: 55e987c87db2e21153582e67dbe60b358a52e35a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661827"
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="10c04-103">Azure AD Connect sync: Directory extensions</span><span class="sxs-lookup"><span data-stu-id="10c04-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="10c04-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10c04-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="10c04-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span><span class="sxs-lookup"><span data-stu-id="10c04-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="10c04-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="10c04-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="10c04-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span><span class="sxs-lookup"><span data-stu-id="10c04-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="10c04-108">At present no Office 365 workload consumes these attributes.</span><span class="sxs-lookup"><span data-stu-id="10c04-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="10c04-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="10c04-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="10c04-110">![Schema Extension Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="10c04-110">![Schema Extension Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="10c04-111">The installation shows the following attributes, which are valid candidates:</span><span class="sxs-lookup"><span data-stu-id="10c04-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="10c04-112">User and Group object types</span><span class="sxs-lookup"><span data-stu-id="10c04-112">User and Group object types</span></span>
* <span data-ttu-id="10c04-113">Single-valued attributes: String, Boolean, Integer, Binary</span><span class="sxs-lookup"><span data-stu-id="10c04-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="10c04-114">Multi-valued attributes: String, Binary</span><span class="sxs-lookup"><span data-stu-id="10c04-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="10c04-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="10c04-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="10c04-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span><span class="sxs-lookup"><span data-stu-id="10c04-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="10c04-117">An object in Azure AD can have up to 100 directory extensions attributes.</span><span class="sxs-lookup"><span data-stu-id="10c04-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="10c04-118">The max length is 250 characters.</span><span class="sxs-lookup"><span data-stu-id="10c04-118">The max length is 250 characters.</span></span> <span data-ttu-id="10c04-119">If an attribute value is longer, then it is truncated by the sync engine.</span><span class="sxs-lookup"><span data-stu-id="10c04-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="10c04-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span><span class="sxs-lookup"><span data-stu-id="10c04-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="10c04-121">You can see this application in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="10c04-121">You can see this application in the Azure portal.</span></span>  
![Schema Extension App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="10c04-123">These attributes are now available through Graph:</span><span class="sxs-lookup"><span data-stu-id="10c04-123">These attributes are now available through Graph:</span></span>  
![Graph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="10c04-125">The attributes are prefixed with extension\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="10c04-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="10c04-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="10c04-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10c04-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="10c04-127">Next steps</span></span>
<span data-ttu-id="10c04-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="10c04-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="10c04-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="10c04-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>



