---
title: Azure App Service Deployment Credentials | Microsoft Docs
description: Learn how to use the Azure App Service deployment credentials.
services: app-service
documentationcenter: ''
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a17260770f0b2e0a73585ce4108bd5625ac22229
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868840"
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="944f9-103">Configure deployment credentials for Azure App Service</span><span class="sxs-lookup"><span data-stu-id="944f9-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="944f9-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="944f9-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="944f9-105">These are not the same as your Azure Active Directory credentials.</span><span class="sxs-lookup"><span data-stu-id="944f9-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="944f9-106">**User-level credentials**: one set of credentials for the entire Azure account.</span><span class="sxs-lookup"><span data-stu-id="944f9-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="944f9-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span><span class="sxs-lookup"><span data-stu-id="944f9-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="944f9-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="944f9-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="944f9-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource page](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="944f9-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource page](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="944f9-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span><span class="sxs-lookup"><span data-stu-id="944f9-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="944f9-111">These deployment credentials should not be shared with other Azure users.</span><span class="sxs-lookup"><span data-stu-id="944f9-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="944f9-112">**App-level credentials**: one set of credentials for each app.</span><span class="sxs-lookup"><span data-stu-id="944f9-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="944f9-113">It can be used to deploy to that app only.</span><span class="sxs-lookup"><span data-stu-id="944f9-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="944f9-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span><span class="sxs-lookup"><span data-stu-id="944f9-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="944f9-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span><span class="sxs-lookup"><span data-stu-id="944f9-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="944f9-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span><span class="sxs-lookup"><span data-stu-id="944f9-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="944f9-117">Readers are not allowed to publish, and hence can't access those credentials.</span><span class="sxs-lookup"><span data-stu-id="944f9-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <a name="userscope"></a><span data-ttu-id="944f9-118">Set and reset user-level credentials</span><span class="sxs-lookup"><span data-stu-id="944f9-118">Set and reset user-level credentials</span></span>

<span data-ttu-id="944f9-119">You can configure your user-level credentials in any app's [resource page](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="944f9-119">You can configure your user-level credentials in any app's [resource page](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="944f9-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span><span class="sxs-lookup"><span data-stu-id="944f9-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="944f9-121">To configure your user-level credentials:</span><span class="sxs-lookup"><span data-stu-id="944f9-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="944f9-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="944f9-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="944f9-123">In the portal, you must have at least one app before you can access the deployment credentials page.</span><span class="sxs-lookup"><span data-stu-id="944f9-123">In the portal, you must have at least one app before you can access the deployment credentials page.</span></span> <span data-ttu-id="944f9-124">However, with the [Azure CLI](/cli/azure/webapp/deployment/user?view=azure-cli-latest#az-webapp-deployment-user-set), you can configure user-level credentials without an existing app.</span><span class="sxs-lookup"><span data-stu-id="944f9-124">However, with the [Azure CLI](/cli/azure/webapp/deployment/user?view=azure-cli-latest#az-webapp-deployment-user-set), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="944f9-125">Configure the user name and password, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="944f9-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="944f9-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span><span class="sxs-lookup"><span data-stu-id="944f9-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="944f9-127">and *FTP* deployment username in your app's **Properties**.</span><span class="sxs-lookup"><span data-stu-id="944f9-127">and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="944f9-128">Azure does not show your user-level deployment password.</span><span class="sxs-lookup"><span data-stu-id="944f9-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="944f9-129">If you forget the password, you can't retrieve it.</span><span class="sxs-lookup"><span data-stu-id="944f9-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="944f9-130">However, you can reset your credentials by following the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="944f9-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <a name="appscope"></a><span data-ttu-id="944f9-131">Get and reset app-level credentials</span><span class="sxs-lookup"><span data-stu-id="944f9-131">Get and reset app-level credentials</span></span>
<span data-ttu-id="944f9-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span><span class="sxs-lookup"><span data-stu-id="944f9-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="944f9-133">To get the app-level credentials:</span><span class="sxs-lookup"><span data-stu-id="944f9-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="944f9-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span><span class="sxs-lookup"><span data-stu-id="944f9-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="944f9-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span><span class="sxs-lookup"><span data-stu-id="944f9-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="944f9-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="944f9-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="944f9-137">Then, get its `userName` and `password` attributes.</span><span class="sxs-lookup"><span data-stu-id="944f9-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="944f9-138">These are the app-level credentials.</span><span class="sxs-lookup"><span data-stu-id="944f9-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="944f9-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="944f9-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="944f9-140">To reset the app-level credentials:</span><span class="sxs-lookup"><span data-stu-id="944f9-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="944f9-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span><span class="sxs-lookup"><span data-stu-id="944f9-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="944f9-142">Click **...More** > **Reset publish profile**.</span><span class="sxs-lookup"><span data-stu-id="944f9-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="944f9-143">Click **Yes** to confirm the reset.</span><span class="sxs-lookup"><span data-stu-id="944f9-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="944f9-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span><span class="sxs-lookup"><span data-stu-id="944f9-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="944f9-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="944f9-145">Next steps</span></span>

<span data-ttu-id="944f9-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="944f9-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
