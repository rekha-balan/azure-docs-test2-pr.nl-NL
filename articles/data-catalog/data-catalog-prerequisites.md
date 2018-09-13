---
title: Azure Data Catalog prerequisites | Microsoft Docs
description: Azure Data Catalog prerequisites - what you need to get started with Azure Data Catalog.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: e4e97d75be89f0c94f4c027c5ec807a08f2906eb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549448"
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="b6dcb-103">Azure Data Catalog prerequisites</span><span class="sxs-lookup"><span data-stu-id="b6dcb-103">Azure Data Catalog prerequisites</span></span>
## <a name="what-do-i-need-to-get-started-with-azure-data-catalog"></a><span data-ttu-id="b6dcb-104">What do I need to get started with Azure Data Catalog?</span><span class="sxs-lookup"><span data-stu-id="b6dcb-104">What do I need to get started with Azure Data Catalog?</span></span>
<span data-ttu-id="b6dcb-105">There are a few things you’ll need to take care of before you can set up **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-105">There are a few things you’ll need to take care of before you can set up **Azure Data Catalog**.</span></span> <span data-ttu-id="b6dcb-106">Don’t worry – they won’t take long!</span><span class="sxs-lookup"><span data-stu-id="b6dcb-106">Don’t worry – they won’t take long!</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="b6dcb-107">Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="b6dcb-107">Azure Subscription</span></span>
<span data-ttu-id="b6dcb-108">To set up Azure Data Catalog, you must be the owner or co-owner of an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-108">To set up Azure Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="b6dcb-109">Azure subscriptions help you organize access to cloud service resources like Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-109">Azure subscriptions help you organize access to cloud service resources like Azure Data Catalog.</span></span> <span data-ttu-id="b6dcb-110">They also help you control how resource usage is reported, billed, and paid for.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-110">They also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="b6dcb-111">Each subscription can have a different billing and payment setup, so you can have different subscriptions and different plans by department, project, regional office, and so on.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-111">Each subscription can have a different billing and payment setup, so you can have different subscriptions and different plans by department, project, regional office, and so on.</span></span> <span data-ttu-id="b6dcb-112">Every cloud service belongs to a subscription, and you need to have a subscription before setting up Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-112">Every cloud service belongs to a subscription, and you need to have a subscription before setting up Azure Data Catalog.</span></span> <span data-ttu-id="b6dcb-113">To learn more, see [Manage Accounts, Subscriptions, and Administrative Roles](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b6dcb-113">To learn more, see [Manage Accounts, Subscriptions, and Administrative Roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="b6dcb-114">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6dcb-114">Azure Active Directory</span></span>
<span data-ttu-id="b6dcb-115">To set up Azure Data Catalog, you must be logged in using an Azure Active Directory user account.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-115">To set up Azure Data Catalog, you must be logged in using an Azure Active Directory user account.</span></span>

<span data-ttu-id="b6dcb-116">Azure Active Directory (Azure AD) provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-116">Azure Active Directory (Azure AD) provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="b6dcb-117">Users can use a single work or school account for single sign-on to any cloud and on-premises web application.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-117">Users can use a single work or school account for single sign-on to any cloud and on-premises web application.</span></span> <span data-ttu-id="b6dcb-118">Azure Data Catalog uses Azure AD to authenticate sign-on.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-118">Azure Data Catalog uses Azure AD to authenticate sign-on.</span></span> <span data-ttu-id="b6dcb-119">To learn more, see [What is Azure Active Directory](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6dcb-119">To learn more, see [What is Azure Active Directory](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b6dcb-120">The [Azure portal](http://portal.azure.com/) allows users to sign in using either a personal Microsoft Account or an Azure Active Directory work or school account.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-120">The [Azure portal](http://portal.azure.com/) allows users to sign in using either a personal Microsoft Account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="b6dcb-121">To set up Azure Data Catalog using the Azure portal or using the [Data Catalog portal](http://www.azuredatacatalog.com) you must be logged in using an Azure Active Directory account, not a personal account.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-121">To set up Azure Data Catalog using the Azure portal or using the [Data Catalog portal](http://www.azuredatacatalog.com) you must be logged in using an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="b6dcb-122">Active Directory policy configuration</span><span class="sxs-lookup"><span data-stu-id="b6dcb-122">Active Directory policy configuration</span></span>
<span data-ttu-id="b6dcb-123">In some situations, users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-123">In some situations, users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span> <span data-ttu-id="b6dcb-124">This problem behavior may occur only when the user is on the company network, or may occur only when the user is connecting from outside the company network.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-124">This problem behavior may occur only when the user is on the company network, or may occur only when the user is connecting from outside the company network.</span></span>

<span data-ttu-id="b6dcb-125">The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-125">The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="b6dcb-126">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-126">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="b6dcb-127">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections, as illustrated below.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-127">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections, as illustrated below.</span></span> <span data-ttu-id="b6dcb-128">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span><span class="sxs-lookup"><span data-stu-id="b6dcb-128">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

 ![Active Directory Global Authentication Policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-prerequisites/global-auth-policy.png)

<span data-ttu-id="b6dcb-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6dcb-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

