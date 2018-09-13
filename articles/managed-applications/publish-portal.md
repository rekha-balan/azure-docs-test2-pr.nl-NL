---
title: Publish an Azure managed application through portal | Microsoft Docs
description: Shows how to use the Azure portal to create an Azure managed application that is intended for members of your organization.
services: managed-applications
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.date: 11/02/2017
ms.author: tomfitz
ms.openlocfilehash: e52acd8587203c4729ac2bcd6e4bbc09620ead86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870781"
---
# <a name="publish-a-service-catalog-application-through-azure-portal"></a><span data-ttu-id="f40db-103">Publish a service catalog application through Azure portal</span><span class="sxs-lookup"><span data-stu-id="f40db-103">Publish a service catalog application through Azure portal</span></span>

<span data-ttu-id="f40db-104">You can use the Azure portal to publish [managed applications](overview.md) that are intended for members of your organization.</span><span class="sxs-lookup"><span data-stu-id="f40db-104">You can use the Azure portal to publish [managed applications](overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="f40db-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span><span class="sxs-lookup"><span data-stu-id="f40db-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="f40db-106">These managed applications are available through the service catalog, not the Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="f40db-106">These managed applications are available through the service catalog, not the Azure marketplace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f40db-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f40db-107">Prerequisites</span></span>

<span data-ttu-id="f40db-108">When publishing a managed application, you specify an identity to manage the resources.</span><span class="sxs-lookup"><span data-stu-id="f40db-108">When publishing a managed application, you specify an identity to manage the resources.</span></span> <span data-ttu-id="f40db-109">We recommend you specify an Azure Active Directory user group.</span><span class="sxs-lookup"><span data-stu-id="f40db-109">We recommend you specify an Azure Active Directory user group.</span></span> <span data-ttu-id="f40db-110">To create an Azure Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f40db-110">To create an Azure Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md).</span></span> 

<span data-ttu-id="f40db-111">The .zip file that contains the managed application definition must be available through a URI.</span><span class="sxs-lookup"><span data-stu-id="f40db-111">The .zip file that contains the managed application definition must be available through a URI.</span></span> <span data-ttu-id="f40db-112">We recommend that you upload your .zip file to a storage blob.</span><span class="sxs-lookup"><span data-stu-id="f40db-112">We recommend that you upload your .zip file to a storage blob.</span></span> 

## <a name="create-managed-application-with-portal"></a><span data-ttu-id="f40db-113">Create managed application with portal</span><span class="sxs-lookup"><span data-stu-id="f40db-113">Create managed application with portal</span></span>

1. <span data-ttu-id="f40db-114">In the upper left corner, select **+ New**.</span><span class="sxs-lookup"><span data-stu-id="f40db-114">In the upper left corner, select **+ New**.</span></span>

   ![New service](./media/publish-portal/new.png)

1. <span data-ttu-id="f40db-116">Search for **service catalog**.</span><span class="sxs-lookup"><span data-stu-id="f40db-116">Search for **service catalog**.</span></span>

1. <span data-ttu-id="f40db-117">In the results, scroll until you find **Service Catalog Managed Application Definition**.</span><span class="sxs-lookup"><span data-stu-id="f40db-117">In the results, scroll until you find **Service Catalog Managed Application Definition**.</span></span> <span data-ttu-id="f40db-118">Select it.</span><span class="sxs-lookup"><span data-stu-id="f40db-118">Select it.</span></span>

   ![Search for managed application definitions](./media/publish-portal/select-managed-apps-definition.png)

1. <span data-ttu-id="f40db-120">Select **Create** to start the process of creating the managed application definition.</span><span class="sxs-lookup"><span data-stu-id="f40db-120">Select **Create** to start the process of creating the managed application definition.</span></span>

   ![Create managed application definition](./media/publish-portal/create-definition.png)

1. <span data-ttu-id="f40db-122">Provide values for name, display name, description, location, subscription, and resource group.</span><span class="sxs-lookup"><span data-stu-id="f40db-122">Provide values for name, display name, description, location, subscription, and resource group.</span></span> <span data-ttu-id="f40db-123">For package file URI, provide the path to the zip file you created.</span><span class="sxs-lookup"><span data-stu-id="f40db-123">For package file URI, provide the path to the zip file you created.</span></span>

   ![Provide values](./media/publish-portal/fill-application-values.png)

1. <span data-ttu-id="f40db-125">When you get to the Authentication and Lock Level section, select **Add Authorization**.</span><span class="sxs-lookup"><span data-stu-id="f40db-125">When you get to the Authentication and Lock Level section, select **Add Authorization**.</span></span>

   ![Add authorization](./media/publish-portal/add-authorization.png)

1. <span data-ttu-id="f40db-127">Select an Azure Active Directory group to manage the resources, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f40db-127">Select an Azure Active Directory group to manage the resources, and select **OK**.</span></span>

   ![Add authorization group](./media/publish-portal/add-auth-group.png)

1. <span data-ttu-id="f40db-129">When you have provided all the values, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f40db-129">When you have provided all the values, select **Create**.</span></span>

   ![Create managed application](./media/publish-portal/create-app.png)

## <a name="next-steps"></a><span data-ttu-id="f40db-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="f40db-131">Next steps</span></span>

* <span data-ttu-id="f40db-132">For an introduction to managed applications, see [Managed application overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f40db-132">For an introduction to managed applications, see [Managed application overview](overview.md).</span></span>
* <span data-ttu-id="f40db-133">For managed application examples, see [Sample projects for Azure managed applications](sample-projects.md).</span><span class="sxs-lookup"><span data-stu-id="f40db-133">For managed application examples, see [Sample projects for Azure managed applications](sample-projects.md).</span></span>
* <span data-ttu-id="f40db-134">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f40db-134">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>