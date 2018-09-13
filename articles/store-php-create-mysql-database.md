---
title: Create and connect to a MySQL database in Azure
description: Learn how to use the Azure portal to create a MySQL database and then connect to it from a PHP web app in Azure.
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: ''
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm;cephalin
ms.openlocfilehash: 13f2f21218753b8bece0bc35279963845a9307d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672006"
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="f46fa-103">Create and connect to a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="f46fa-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="f46fa-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f46fa-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f46fa-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="f46fa-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="f46fa-106">Create a MySQL database in Azure portal</span><span class="sxs-lookup"><span data-stu-id="f46fa-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="f46fa-107">To create a MySQL database in the Azure portal, do the following:</span><span class="sxs-lookup"><span data-stu-id="f46fa-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="f46fa-108">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f46fa-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f46fa-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span><span class="sxs-lookup"><span data-stu-id="f46fa-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Create a MySQL database in Azure - start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="f46fa-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span><span class="sxs-lookup"><span data-stu-id="f46fa-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="f46fa-112">**Database Name**: Type a uniquely identifiable name</span><span class="sxs-lookup"><span data-stu-id="f46fa-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="f46fa-113">**Subscription**: Choose the subscription to use</span><span class="sxs-lookup"><span data-stu-id="f46fa-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="f46fa-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span><span class="sxs-lookup"><span data-stu-id="f46fa-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="f46fa-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span><span class="sxs-lookup"><span data-stu-id="f46fa-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="f46fa-116">Resources in the same group can be easily managed together.</span><span class="sxs-lookup"><span data-stu-id="f46fa-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="f46fa-117">**Location**: Select a location close to you.</span><span class="sxs-lookup"><span data-stu-id="f46fa-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="f46fa-118">When adding to an existing resource group, you're locked to the resource group's location.</span><span class="sxs-lookup"><span data-stu-id="f46fa-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="f46fa-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="f46fa-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="f46fa-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="f46fa-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="f46fa-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="f46fa-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="f46fa-122">This is especially helpful if you aren't familiar with portal navigation yet.</span><span class="sxs-lookup"><span data-stu-id="f46fa-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="f46fa-123">The following screenshot is just an example of how you can configure your MySQL database.</span><span class="sxs-lookup"><span data-stu-id="f46fa-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Create a MySQL database in Azure - configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="f46fa-125">When you're done configuring, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f46fa-125">When you're done configuring, click **Create**.</span></span>

    ![Create a MySQL database in Azure - create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="f46fa-127">You will see a pop-up notification letting you know that deployment has started.</span><span class="sxs-lookup"><span data-stu-id="f46fa-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Create a MySQL database in Azure - in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="f46fa-129">You will get another pop-up once deployment has succeeded.</span><span class="sxs-lookup"><span data-stu-id="f46fa-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="f46fa-130">The portal will also open your MySQL database blade automatically.</span><span class="sxs-lookup"><span data-stu-id="f46fa-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="f46fa-131">Connect to your MySQL database</span><span class="sxs-lookup"><span data-stu-id="f46fa-131">Connect to your MySQL database</span></span>
<span data-ttu-id="f46fa-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span><span class="sxs-lookup"><span data-stu-id="f46fa-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Create a MySQL database in Azure - MySQL database blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="f46fa-134">You can now use that connection information in any web app.</span><span class="sxs-lookup"><span data-stu-id="f46fa-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="f46fa-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="f46fa-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="f46fa-136">Connect a Laravel web app (from the PHP get started tutorial)</span><span class="sxs-lookup"><span data-stu-id="f46fa-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="f46fa-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span><span class="sxs-lookup"><span data-stu-id="f46fa-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="f46fa-138">You can easily add database capabilities to your Laravel app.</span><span class="sxs-lookup"><span data-stu-id="f46fa-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="f46fa-139">Just follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="f46fa-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="f46fa-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f46fa-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="f46fa-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="f46fa-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="f46fa-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span><span class="sxs-lookup"><span data-stu-id="f46fa-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="f46fa-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span><span class="sxs-lookup"><span data-stu-id="f46fa-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="f46fa-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span><span class="sxs-lookup"><span data-stu-id="f46fa-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Create a MySQL database in Azure - in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="f46fa-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="f46fa-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="f46fa-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span><span class="sxs-lookup"><span data-stu-id="f46fa-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="f46fa-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span><span class="sxs-lookup"><span data-stu-id="f46fa-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="f46fa-149">Run the development server now:</span><span class="sxs-lookup"><span data-stu-id="f46fa-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="f46fa-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span><span class="sxs-lookup"><span data-stu-id="f46fa-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Connect to MySQL database in Azure - register user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="f46fa-152">Follow the UI prompt complete the registration.</span><span class="sxs-lookup"><span data-stu-id="f46fa-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="f46fa-153">Once registration completes, you will be logged in.</span><span class="sxs-lookup"><span data-stu-id="f46fa-153">Once registration completes, you will be logged in.</span></span>

    ![Connect to MySQL database in Azure - register user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="f46fa-155">You are now developing your app against the MySQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="f46fa-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="f46fa-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f46fa-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="f46fa-157">Run the following Azure CLI commands:</span><span class="sxs-lookup"><span data-stu-id="f46fa-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

    <span data-ttu-id="f46fa-158">Find out how this works in [Configure the Azure web app](app-service-web/app-service-web-get-started-php.md#configure-to-use-php).</span><span class="sxs-lookup"><span data-stu-id="f46fa-158">Find out how this works in [Configure the Azure web app](app-service-web/app-service-web-get-started-php.md#configure-to-use-php).</span></span>
6. <span data-ttu-id="f46fa-159">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="f46fa-159">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="f46fa-160">Browse to the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f46fa-160">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="f46fa-161">Log in using the user credentials you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f46fa-161">Log in using the user credentials you created earlier.</span></span>

    ![Connect to MySQL database in Azure - browse to Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="f46fa-163">After you log in, you should see the friendly post-login screen.</span><span class="sxs-lookup"><span data-stu-id="f46fa-163">After you log in, you should see the friendly post-login screen.</span></span>

    ![Connect to MySQL database in Azure - logged in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="f46fa-165">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span><span class="sxs-lookup"><span data-stu-id="f46fa-165">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f46fa-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="f46fa-166">Next steps</span></span>
<span data-ttu-id="f46fa-167">For more information, see the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f46fa-167">For more information, see the [PHP Developer Center](/develop/php/).</span></span>










