---
title: Tutorial - Create an Azure Active Directory B2C tenant | Microsoft Docs
description: Learn how to prepare for registering your applications by creating an Azure Active Directory B2C tenant using the Azure portal.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory-b2c
ms.workload: identity
ms.topic: conceptual
ms.date: 06/19/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: cc48cd3eb40d93c26a68caf843a89f7bbfb46c6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865355"
---
# <a name="tutorial-create-an-azure-active-directory-b2c-tenant"></a><span data-ttu-id="e8164-103">Tutorial: Create an Azure Active Directory B2C tenant</span><span class="sxs-lookup"><span data-stu-id="e8164-103">Tutorial: Create an Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="e8164-104">Before your applications can interact with Azure Active Directory (Azure AD) B2C, they must be registered in a tenant that you manage.</span><span class="sxs-lookup"><span data-stu-id="e8164-104">Before your applications can interact with Azure Active Directory (Azure AD) B2C, they must be registered in a tenant that you manage.</span></span>

<span data-ttu-id="e8164-105">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e8164-105">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8164-106">Create an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="e8164-106">Create an Azure AD B2C tenant</span></span>
> * <span data-ttu-id="e8164-107">Link your tenant to your subscription</span><span class="sxs-lookup"><span data-stu-id="e8164-107">Link your tenant to your subscription</span></span>

<span data-ttu-id="e8164-108">You learn how to register an application in the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="e8164-108">You learn how to register an application in the next tutorial.</span></span>

<span data-ttu-id="e8164-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e8164-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="e8164-110">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e8164-110">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="e8164-111">Create an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="e8164-111">Create an Azure AD B2C tenant</span></span>

1. <span data-ttu-id="e8164-112">Choose **Create a resource** in the top-left corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8164-112">Choose **Create a resource** in the top-left corner of the Azure portal.</span></span>
2. <span data-ttu-id="e8164-113">In the search box above the list of Azure Marketplace resources, search for and select **Active Directory B2C**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8164-113">In the search box above the list of Azure Marketplace resources, search for and select **Active Directory B2C**, and then click **Create**.</span></span>
3. <span data-ttu-id="e8164-114">Choose **Create a new Azure AD B2C Tenant**, enter an organization name and initial domain name, which is used in the tenant name, select the country, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8164-114">Choose **Create a new Azure AD B2C Tenant**, enter an organization name and initial domain name, which is used in the tenant name, select the country, and then click **Create**.</span></span> <span data-ttu-id="e8164-115">Be sure of the country of the tenant because it can't be changed later.</span><span class="sxs-lookup"><span data-stu-id="e8164-115">Be sure of the country of the tenant because it can't be changed later.</span></span>

    ![Create a tenant](./media/tutorial-create-tenant/create-tenant.png)

    <span data-ttu-id="e8164-117">In this example the tenant name is contoso0522Tenant.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="e8164-117">In this example the tenant name is contoso0522Tenant.onmicrosoft.com</span></span>

<span data-ttu-id="e8164-118">To start managing your new tenant, click the word **here** where it says **Click here, to manage your new directory**.</span><span class="sxs-lookup"><span data-stu-id="e8164-118">To start managing your new tenant, click the word **here** where it says **Click here, to manage your new directory**.</span></span> <span data-ttu-id="e8164-119">You will see a **Troubleshoot** message that says you need to link your subscription to the new tenant.</span><span class="sxs-lookup"><span data-stu-id="e8164-119">You will see a **Troubleshoot** message that says you need to link your subscription to the new tenant.</span></span> 

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="e8164-120">Link your tenant to your subscription</span><span class="sxs-lookup"><span data-stu-id="e8164-120">Link your tenant to your subscription</span></span>

<span data-ttu-id="e8164-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all functionality and pay for usage charges.</span><span class="sxs-lookup"><span data-stu-id="e8164-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all functionality and pay for usage charges.</span></span> <span data-ttu-id="e8164-122">If you don't link your tenant to your subscription, your applications won't work correctly.</span><span class="sxs-lookup"><span data-stu-id="e8164-122">If you don't link your tenant to your subscription, your applications won't work correctly.</span></span>

1. <span data-ttu-id="e8164-123">Make sure you're using the directory that contains the subscription you want to associate to the new tenant by switching the directory in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8164-123">Make sure you're using the directory that contains the subscription you want to associate to the new tenant by switching the directory in the top-right corner of the Azure portal.</span></span>

    ![Switch directories](./media/tutorial-create-tenant/switch-directories.png)

    <span data-ttu-id="e8164-125">And then selecting the directory that contains your subscription.</span><span class="sxs-lookup"><span data-stu-id="e8164-125">And then selecting the directory that contains your subscription.</span></span>

    ![Select directory](./media/tutorial-create-tenant/select-directory.png)

2. <span data-ttu-id="e8164-127">Choose **Create a resource** in the upper top-left corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e8164-127">Choose **Create a resource** in the upper top-left corner of the Azure portal.</span></span>
3. <span data-ttu-id="e8164-128">In the search box above the list of Azure Marketplace resources, search for and select **Active Directory B2C**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8164-128">In the search box above the list of Azure Marketplace resources, search for and select **Active Directory B2C**, and then click **Create**.</span></span>
4. <span data-ttu-id="e8164-129">Choose **Link an existing Azure AD B2C Tenant to my Azure subscription**, select the tenant that you created, select your subscription, enter *myContosoTenantRG* for the resource group name, accept the location, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8164-129">Choose **Link an existing Azure AD B2C Tenant to my Azure subscription**, select the tenant that you created, select your subscription, enter *myContosoTenantRG* for the resource group name, accept the location, and then click **Create**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8164-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8164-130">Next steps</span></span>

<span data-ttu-id="e8164-131">In this article, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="e8164-131">In this article, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8164-132">Create an Azure AD B2C tenant</span><span class="sxs-lookup"><span data-stu-id="e8164-132">Create an Azure AD B2C tenant</span></span>
> * <span data-ttu-id="e8164-133">Link your tenant to your subscription</span><span class="sxs-lookup"><span data-stu-id="e8164-133">Link your tenant to your subscription</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8164-134">Enable a web application to authenticate with accounts</span><span class="sxs-lookup"><span data-stu-id="e8164-134">Enable a web application to authenticate with accounts</span></span>](active-directory-b2c-tutorials-web-app.md)