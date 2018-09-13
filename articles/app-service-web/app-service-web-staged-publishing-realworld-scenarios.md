---
title: Use DevOps environments effectively for your web app | Microsoft Docs
description: Learn how to use deployment slots to set up and manage multiple development environments for your application
services: app-service\web
documentationcenter: ''
author: sunbuild
manager: yochayk
editor: ''
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: f240c3a2ba7b1e810bfd341e1d076b041ffae645
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551086"
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="72507-103">Use DevOps environments effectively for your web apps</span><span class="sxs-lookup"><span data-stu-id="72507-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="72507-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span><span class="sxs-lookup"><span data-stu-id="72507-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="72507-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span><span class="sxs-lookup"><span data-stu-id="72507-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="72507-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span><span class="sxs-lookup"><span data-stu-id="72507-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="72507-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span><span class="sxs-lookup"><span data-stu-id="72507-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="72507-108">Set up a non-production environment (stage, dev, QA)</span><span class="sxs-lookup"><span data-stu-id="72507-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="72507-109">After a production web app is up and running, the next step is to create a non-production environment.</span><span class="sxs-lookup"><span data-stu-id="72507-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="72507-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span><span class="sxs-lookup"><span data-stu-id="72507-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="72507-111">Deployment slots are live web apps that have their own host names.</span><span class="sxs-lookup"><span data-stu-id="72507-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="72507-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span><span class="sxs-lookup"><span data-stu-id="72507-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="72507-113">When you deploy your application to a deployment slot, you get the following benefits:</span><span class="sxs-lookup"><span data-stu-id="72507-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="72507-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span><span class="sxs-lookup"><span data-stu-id="72507-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="72507-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span><span class="sxs-lookup"><span data-stu-id="72507-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="72507-116">This process eliminates downtime when you deploy your web app.</span><span class="sxs-lookup"><span data-stu-id="72507-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="72507-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span><span class="sxs-lookup"><span data-stu-id="72507-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="72507-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span><span class="sxs-lookup"><span data-stu-id="72507-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="72507-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span><span class="sxs-lookup"><span data-stu-id="72507-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="72507-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span><span class="sxs-lookup"><span data-stu-id="72507-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="72507-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="72507-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="72507-122">Every environment should include its own set of resources.</span><span class="sxs-lookup"><span data-stu-id="72507-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="72507-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span><span class="sxs-lookup"><span data-stu-id="72507-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="72507-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span><span class="sxs-lookup"><span data-stu-id="72507-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="72507-125">Examples of using multiple development environments</span><span class="sxs-lookup"><span data-stu-id="72507-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="72507-126">Any project should follow source code management with at least two environments: development and production.</span><span class="sxs-lookup"><span data-stu-id="72507-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="72507-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span><span class="sxs-lookup"><span data-stu-id="72507-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="72507-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span><span class="sxs-lookup"><span data-stu-id="72507-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="72507-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span><span class="sxs-lookup"><span data-stu-id="72507-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="72507-130">How do you break the content out into different environments?</span><span class="sxs-lookup"><span data-stu-id="72507-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="72507-131">What files can you change without affecting framework version updates?</span><span class="sxs-lookup"><span data-stu-id="72507-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="72507-132">How do you manage configurations per environment?</span><span class="sxs-lookup"><span data-stu-id="72507-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="72507-133">How do you manage version updates for modules, plugins, and the core framework?</span><span class="sxs-lookup"><span data-stu-id="72507-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="72507-134">There are many ways to set up multiple environments for your project.</span><span class="sxs-lookup"><span data-stu-id="72507-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="72507-135">The following examples show one method for each respective application.</span><span class="sxs-lookup"><span data-stu-id="72507-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="72507-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="72507-136">WordPress</span></span>
<span data-ttu-id="72507-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span><span class="sxs-lookup"><span data-stu-id="72507-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="72507-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span><span class="sxs-lookup"><span data-stu-id="72507-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="72507-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span><span class="sxs-lookup"><span data-stu-id="72507-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="72507-140">Before you create a staging slot, set up your application code to support multiple environments.</span><span class="sxs-lookup"><span data-stu-id="72507-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="72507-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span><span class="sxs-lookup"><span data-stu-id="72507-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="72507-142">This process will enable your application to pick the correct configuration based on the selected environment.</span><span class="sxs-lookup"><span data-stu-id="72507-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="72507-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span><span class="sxs-lookup"><span data-stu-id="72507-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="72507-144">Copy the following in `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="72507-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    <span data-ttu-id="72507-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span><span class="sxs-lookup"><span data-stu-id="72507-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="72507-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span><span class="sxs-lookup"><span data-stu-id="72507-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="72507-147">Copy the following code in `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="72507-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a><span data-ttu-id="72507-148">Use relative paths</span><span class="sxs-lookup"><span data-stu-id="72507-148">Use relative paths</span></span>
<span data-ttu-id="72507-149">One last thing to configure in the WordPress app is relative paths.</span><span class="sxs-lookup"><span data-stu-id="72507-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="72507-150">WordPress stores URL information in the database.</span><span class="sxs-lookup"><span data-stu-id="72507-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="72507-151">This storage makes moving content from one environment to another more difficult.</span><span class="sxs-lookup"><span data-stu-id="72507-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="72507-152">You need to update the database every time you move from local to stage or stage to production environments.</span><span class="sxs-lookup"><span data-stu-id="72507-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="72507-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span><span class="sxs-lookup"><span data-stu-id="72507-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="72507-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span><span class="sxs-lookup"><span data-stu-id="72507-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="72507-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span><span class="sxs-lookup"><span data-stu-id="72507-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="72507-156">Save your permalink settings for WordPress app.</span><span class="sxs-lookup"><span data-stu-id="72507-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="72507-157">The final `wp-config.php` file</span><span class="sxs-lookup"><span data-stu-id="72507-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="72507-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span><span class="sxs-lookup"><span data-stu-id="72507-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="72507-159">Here's a final version of the `wp-config.php` file:</span><span class="sxs-lookup"><span data-stu-id="72507-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="72507-160">Set up a staging environment</span><span class="sxs-lookup"><span data-stu-id="72507-160">Set up a staging environment</span></span>
1. <span data-ttu-id="72507-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="72507-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="72507-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="72507-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="72507-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="72507-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="72507-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span><span class="sxs-lookup"><span data-stu-id="72507-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="72507-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span><span class="sxs-lookup"><span data-stu-id="72507-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![Create stage deployment slot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="72507-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="72507-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![Add MySQL database to resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="72507-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="72507-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="72507-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span><span class="sxs-lookup"><span data-stu-id="72507-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="72507-171">Configure environment-specific app settings</span><span class="sxs-lookup"><span data-stu-id="72507-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="72507-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span><span class="sxs-lookup"><span data-stu-id="72507-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="72507-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span><span class="sxs-lookup"><span data-stu-id="72507-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="72507-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="72507-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="72507-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span><span class="sxs-lookup"><span data-stu-id="72507-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="72507-176">WordPress version upgrade</span><span class="sxs-lookup"><span data-stu-id="72507-176">WordPress version upgrade</span></span>
* <span data-ttu-id="72507-177">Add new or edit or upgrade plugins</span><span class="sxs-lookup"><span data-stu-id="72507-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="72507-178">Add new or edit or upgrade themes</span><span class="sxs-lookup"><span data-stu-id="72507-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="72507-179">Configure app settings for:</span><span class="sxs-lookup"><span data-stu-id="72507-179">Configure app settings for:</span></span>

* <span data-ttu-id="72507-180">Database information</span><span class="sxs-lookup"><span data-stu-id="72507-180">Database information</span></span>
* <span data-ttu-id="72507-181">Turning on/off WordPress logging</span><span class="sxs-lookup"><span data-stu-id="72507-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="72507-182">WordPress security settings</span><span class="sxs-lookup"><span data-stu-id="72507-182">WordPress security settings</span></span>

![App Settings for Wordpress web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="72507-184">Make sure that you add the following app settings for your production web app and stage slot.</span><span class="sxs-lookup"><span data-stu-id="72507-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="72507-185">Note that the production web app and staging web app use different databases.</span><span class="sxs-lookup"><span data-stu-id="72507-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="72507-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="72507-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="72507-187">This process will swap the configuration for your web app, file content, and database.</span><span class="sxs-lookup"><span data-stu-id="72507-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="72507-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span><span class="sxs-lookup"><span data-stu-id="72507-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="72507-189">Any database changes that are present will not break your production web app.</span><span class="sxs-lookup"><span data-stu-id="72507-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="72507-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="72507-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Web Matrix Publish dialog for WordPress web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="72507-192">Browse and test your staging web app.</span><span class="sxs-lookup"><span data-stu-id="72507-192">Browse and test your staging web app.</span></span> <span data-ttu-id="72507-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span><span class="sxs-lookup"><span data-stu-id="72507-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![Browse staging web app before swapping slots](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="72507-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span><span class="sxs-lookup"><span data-stu-id="72507-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="72507-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span><span class="sxs-lookup"><span data-stu-id="72507-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![Swap preview changes for WordPress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="72507-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span><span class="sxs-lookup"><span data-stu-id="72507-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="72507-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span><span class="sxs-lookup"><span data-stu-id="72507-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="72507-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span><span class="sxs-lookup"><span data-stu-id="72507-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="72507-201">Before doing a **Swap**, here is the production WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="72507-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="72507-202">![Production web app before swapping slots](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="72507-202">![Production web app before swapping slots](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="72507-203">After the **Swap** operation, the theme has been updated on your production web app.</span><span class="sxs-lookup"><span data-stu-id="72507-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![Production web app after swapping slots](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="72507-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span><span class="sxs-lookup"><span data-stu-id="72507-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="72507-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span><span class="sxs-lookup"><span data-stu-id="72507-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="72507-207">The current database might be the previous production database or the stage database.</span><span class="sxs-lookup"><span data-stu-id="72507-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="72507-208">Summary</span><span class="sxs-lookup"><span data-stu-id="72507-208">Summary</span></span>
<span data-ttu-id="72507-209">Following is a generalized process for any application that has a database:</span><span class="sxs-lookup"><span data-stu-id="72507-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="72507-210">Install the application on your local environment.</span><span class="sxs-lookup"><span data-stu-id="72507-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="72507-211">Include environment-specific configurations (local and Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="72507-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="72507-212">Set up your staging and production environments for Web Apps.</span><span class="sxs-lookup"><span data-stu-id="72507-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="72507-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span><span class="sxs-lookup"><span data-stu-id="72507-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="72507-214">Develop your application on your local environment.</span><span class="sxs-lookup"><span data-stu-id="72507-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="72507-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span><span class="sxs-lookup"><span data-stu-id="72507-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="72507-216">Deploy to the staging environment and test.</span><span class="sxs-lookup"><span data-stu-id="72507-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="72507-217">Deploy to production environment.</span><span class="sxs-lookup"><span data-stu-id="72507-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="72507-218">Repeat steps 4 through 6.</span><span class="sxs-lookup"><span data-stu-id="72507-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="72507-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="72507-219">Umbraco</span></span>
<span data-ttu-id="72507-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span><span class="sxs-lookup"><span data-stu-id="72507-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="72507-221">This example provides a different approach to managing multiple development environments.</span><span class="sxs-lookup"><span data-stu-id="72507-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="72507-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span><span class="sxs-lookup"><span data-stu-id="72507-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="72507-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span><span class="sxs-lookup"><span data-stu-id="72507-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="72507-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="72507-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="72507-225">Create an Umbraco web app with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72507-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="72507-226">Create an Umbraco web app with WebMatrix</span><span class="sxs-lookup"><span data-stu-id="72507-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="72507-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span><span class="sxs-lookup"><span data-stu-id="72507-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="72507-228">This tutorial uses WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="72507-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="72507-229">Set up a staging environment</span><span class="sxs-lookup"><span data-stu-id="72507-229">Set up a staging environment</span></span>
1. <span data-ttu-id="72507-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span><span class="sxs-lookup"><span data-stu-id="72507-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="72507-231">If you do not, you can create one from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="72507-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="72507-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span><span class="sxs-lookup"><span data-stu-id="72507-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="72507-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span><span class="sxs-lookup"><span data-stu-id="72507-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![Update Connection string for staging web app with new staging database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="72507-235">Click **Get Publish settings** for the deployment slot **stage**.</span><span class="sxs-lookup"><span data-stu-id="72507-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="72507-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="72507-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![Get publish setting of the staging web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="72507-238">Open your local development web app in WebMatrix or Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="72507-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="72507-239">This tutorial uses WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="72507-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="72507-240">First, you need to import the publish settings file for your staging web app.</span><span class="sxs-lookup"><span data-stu-id="72507-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![Import Publish settings for Umbraco using Web Matrix](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="72507-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span><span class="sxs-lookup"><span data-stu-id="72507-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="72507-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span><span class="sxs-lookup"><span data-stu-id="72507-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="72507-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span><span class="sxs-lookup"><span data-stu-id="72507-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Review Publish changes in web matrix](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="72507-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span><span class="sxs-lookup"><span data-stu-id="72507-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="72507-247">Set up the Courier2 deployment module</span><span class="sxs-lookup"><span data-stu-id="72507-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="72507-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span><span class="sxs-lookup"><span data-stu-id="72507-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="72507-249">This process reduces the risk of breaking your production web app when you deploy an update.</span><span class="sxs-lookup"><span data-stu-id="72507-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="72507-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="72507-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="72507-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span><span class="sxs-lookup"><span data-stu-id="72507-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![Drop license file under bin folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="72507-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="72507-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="72507-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span><span class="sxs-lookup"><span data-stu-id="72507-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Umbraco Package installer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="72507-256">Upload the Courier2 package by using the installer.</span><span class="sxs-lookup"><span data-stu-id="72507-256">Upload the Courier2 package by using the installer.</span></span>

    ![Upload package for courier module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="72507-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span><span class="sxs-lookup"><span data-stu-id="72507-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="72507-259">Under `<repositories>`, enter the production site URL and user information.</span><span class="sxs-lookup"><span data-stu-id="72507-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="72507-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span><span class="sxs-lookup"><span data-stu-id="72507-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="72507-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span><span class="sxs-lookup"><span data-stu-id="72507-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="72507-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="72507-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="72507-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span><span class="sxs-lookup"><span data-stu-id="72507-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="72507-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span><span class="sxs-lookup"><span data-stu-id="72507-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="72507-265">You should see the repository name as mentioned in `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="72507-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="72507-266">Do this process on both your production and staging web apps.</span><span class="sxs-lookup"><span data-stu-id="72507-266">Do this process on both your production and staging web apps.</span></span>

    ![View destination web app repository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="72507-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span><span class="sxs-lookup"><span data-stu-id="72507-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="72507-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span><span class="sxs-lookup"><span data-stu-id="72507-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Change Title of page and publish](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="72507-271">Right-click the modified page to view all the options.</span><span class="sxs-lookup"><span data-stu-id="72507-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="72507-272">Click **Courier** to open the **Deployment** dialog box.</span><span class="sxs-lookup"><span data-stu-id="72507-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="72507-273">Click **Deploy** to initiate deployment.</span><span class="sxs-lookup"><span data-stu-id="72507-273">Click **Deploy** to initiate deployment.</span></span>

    ![Courier module deployment dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="72507-275">Review the changes, and then click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="72507-275">Review the changes, and then click **Continue**.</span></span>

    ![Courier module deployment dialog review changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="72507-277">The deployment log shows if the deployment was successful.</span><span class="sxs-lookup"><span data-stu-id="72507-277">The deployment log shows if the deployment was successful.</span></span>

     ![View Deployment logs from Courier module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="72507-279">Browse your production web app to see if the changes are reflected.</span><span class="sxs-lookup"><span data-stu-id="72507-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![Browse production web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="72507-281">To learn more about how to use Courier, review the documentation.</span><span class="sxs-lookup"><span data-stu-id="72507-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="72507-282">How to upgrade the Umbraco CMS version</span><span class="sxs-lookup"><span data-stu-id="72507-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="72507-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span><span class="sxs-lookup"><span data-stu-id="72507-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="72507-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span><span class="sxs-lookup"><span data-stu-id="72507-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="72507-285">Here are best practices:</span><span class="sxs-lookup"><span data-stu-id="72507-285">Here are best practices:</span></span>

* <span data-ttu-id="72507-286">Always back up your web app and database before you upgrade.</span><span class="sxs-lookup"><span data-stu-id="72507-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="72507-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span><span class="sxs-lookup"><span data-stu-id="72507-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="72507-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="72507-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="72507-289">Check if packages from partners are compatible with the version you're upgrading to.</span><span class="sxs-lookup"><span data-stu-id="72507-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="72507-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span><span class="sxs-lookup"><span data-stu-id="72507-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="72507-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="72507-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="72507-292">After your local development site is upgraded, publish the changes to the staging web app.</span><span class="sxs-lookup"><span data-stu-id="72507-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="72507-293">Test your application.</span><span class="sxs-lookup"><span data-stu-id="72507-293">Test your application.</span></span> <span data-ttu-id="72507-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span><span class="sxs-lookup"><span data-stu-id="72507-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="72507-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span><span class="sxs-lookup"><span data-stu-id="72507-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="72507-296">This **Swap** operation swaps the web apps and databases.</span><span class="sxs-lookup"><span data-stu-id="72507-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="72507-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span><span class="sxs-lookup"><span data-stu-id="72507-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![Swap preview for deploying Umbraco CMS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="72507-299">Here are advantages of swapping both the web app and the database:</span><span class="sxs-lookup"><span data-stu-id="72507-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="72507-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span><span class="sxs-lookup"><span data-stu-id="72507-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="72507-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span><span class="sxs-lookup"><span data-stu-id="72507-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="72507-302">Many things can go wrong when you deploy files and databases.</span><span class="sxs-lookup"><span data-stu-id="72507-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="72507-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span><span class="sxs-lookup"><span data-stu-id="72507-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="72507-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span><span class="sxs-lookup"><span data-stu-id="72507-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="72507-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span><span class="sxs-lookup"><span data-stu-id="72507-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="72507-306">References</span><span class="sxs-lookup"><span data-stu-id="72507-306">References</span></span>
[<span data-ttu-id="72507-307">Agile software development with Azure App Service</span><span class="sxs-lookup"><span data-stu-id="72507-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="72507-308">Set up staging environments for web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="72507-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="72507-309">How to block web access to non-production deployment slots</span><span class="sxs-lookup"><span data-stu-id="72507-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)






















