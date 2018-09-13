---
title: Log in to Azure from the CLI | Microsoft Docs
description: Connect to your Azure subscription from the Azure Command-Line Interface (Azure CLI) for Mac, Linux, and Windows
editor: tysonn
manager: timlt
documentationcenter: ''
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": ''
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670503"
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="b637f-103">Log in to Azure from the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b637f-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="b637f-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span><span class="sxs-lookup"><span data-stu-id="b637f-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="b637f-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="b637f-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="b637f-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b637f-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="b637f-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="b637f-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="b637f-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span><span class="sxs-lookup"><span data-stu-id="b637f-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="b637f-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="b637f-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="b637f-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b637f-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="b637f-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b637f-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="b637f-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="b637f-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="b637f-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="b637f-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="b637f-114">Scenario 1: azure login with interactive login</span><span class="sxs-lookup"><span data-stu-id="b637f-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="b637f-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span><span class="sxs-lookup"><span data-stu-id="b637f-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="b637f-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span><span class="sxs-lookup"><span data-stu-id="b637f-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="b637f-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span><span class="sxs-lookup"><span data-stu-id="b637f-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="b637f-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b637f-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="b637f-119">The output appears something like the following:</span><span class="sxs-lookup"><span data-stu-id="b637f-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="b637f-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span><span class="sxs-lookup"><span data-stu-id="b637f-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="b637f-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span><span class="sxs-lookup"><span data-stu-id="b637f-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="b637f-122">When that process completes, the command shell completes the login.</span><span class="sxs-lookup"><span data-stu-id="b637f-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="b637f-123">It might look something like:</span><span class="sxs-lookup"><span data-stu-id="b637f-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="b637f-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b637f-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="b637f-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span><span class="sxs-lookup"><span data-stu-id="b637f-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="b637f-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span><span class="sxs-lookup"><span data-stu-id="b637f-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="b637f-127">Scenario 2: azure login with a username and password</span><span class="sxs-lookup"><span data-stu-id="b637f-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="b637f-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span><span class="sxs-lookup"><span data-stu-id="b637f-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="b637f-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span><span class="sxs-lookup"><span data-stu-id="b637f-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="b637f-130">The following example passes the username of an organizational account:</span><span class="sxs-lookup"><span data-stu-id="b637f-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="b637f-131">You are then prompted to enter your password:</span><span class="sxs-lookup"><span data-stu-id="b637f-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="b637f-132">The login process then completes.</span><span class="sxs-lookup"><span data-stu-id="b637f-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="b637f-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span><span class="sxs-lookup"><span data-stu-id="b637f-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="b637f-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span><span class="sxs-lookup"><span data-stu-id="b637f-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="b637f-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span><span class="sxs-lookup"><span data-stu-id="b637f-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="b637f-136">Scenario 3: azure login with a service principal</span><span class="sxs-lookup"><span data-stu-id="b637f-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="b637f-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span><span class="sxs-lookup"><span data-stu-id="b637f-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="b637f-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span><span class="sxs-lookup"><span data-stu-id="b637f-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="b637f-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span><span class="sxs-lookup"><span data-stu-id="b637f-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="b637f-140">You are then prompted to provide the password.</span><span class="sxs-lookup"><span data-stu-id="b637f-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="b637f-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span><span class="sxs-lookup"><span data-stu-id="b637f-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="b637f-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b637f-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="b637f-143">Scenario 4: Use a publish settings file</span><span class="sxs-lookup"><span data-stu-id="b637f-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="b637f-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span><span class="sxs-lookup"><span data-stu-id="b637f-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="b637f-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span><span class="sxs-lookup"><span data-stu-id="b637f-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="b637f-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="b637f-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="b637f-147">Then run the following command:</span><span class="sxs-lookup"><span data-stu-id="b637f-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="b637f-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b637f-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b637f-149">After you sign in, a `.publishsettings` file downloads.</span><span class="sxs-lookup"><span data-stu-id="b637f-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="b637f-150">Make note of where this file is saved.</span><span class="sxs-lookup"><span data-stu-id="b637f-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="b637f-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span><span class="sxs-lookup"><span data-stu-id="b637f-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="b637f-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span><span class="sxs-lookup"><span data-stu-id="b637f-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="b637f-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span><span class="sxs-lookup"><span data-stu-id="b637f-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="b637f-154">Use the provided link to return to the selection page.</span><span class="sxs-lookup"><span data-stu-id="b637f-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="b637f-155">**To import the publish settings file**, run the following command:</span><span class="sxs-lookup"><span data-stu-id="b637f-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="b637f-156">After importing your publish settings, you should delete the `.publishsettings` file.</span><span class="sxs-lookup"><span data-stu-id="b637f-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="b637f-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span><span class="sxs-lookup"><span data-stu-id="b637f-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="b637f-158">CLI command modes</span><span class="sxs-lookup"><span data-stu-id="b637f-158">CLI command modes</span></span>
<span data-ttu-id="b637f-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span><span class="sxs-lookup"><span data-stu-id="b637f-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="b637f-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="b637f-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="b637f-161">To set this mode, run `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b637f-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="b637f-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="b637f-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="b637f-163">To set this mode, run `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="b637f-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="b637f-164">When first installed, the current release of the CLI is in Resource Manager mode.</span><span class="sxs-lookup"><span data-stu-id="b637f-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="b637f-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span><span class="sxs-lookup"><span data-stu-id="b637f-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="b637f-166">That is, resources created in one mode cannot be managed from the other mode.</span><span class="sxs-lookup"><span data-stu-id="b637f-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="b637f-167">Multiple subscriptions</span><span class="sxs-lookup"><span data-stu-id="b637f-167">Multiple subscriptions</span></span>
<span data-ttu-id="b637f-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="b637f-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="b637f-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span><span class="sxs-lookup"><span data-stu-id="b637f-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="b637f-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span><span class="sxs-lookup"><span data-stu-id="b637f-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="b637f-171">This command returns information similar to the following:</span><span class="sxs-lookup"><span data-stu-id="b637f-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="b637f-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="b637f-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="b637f-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span><span class="sxs-lookup"><span data-stu-id="b637f-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="b637f-174">For example:</span><span class="sxs-lookup"><span data-stu-id="b637f-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="b637f-175">This changes the default subscription to Azure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="b637f-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="b637f-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span><span class="sxs-lookup"><span data-stu-id="b637f-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="b637f-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span><span class="sxs-lookup"><span data-stu-id="b637f-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="b637f-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span><span class="sxs-lookup"><span data-stu-id="b637f-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="b637f-179">Storage of CLI settings</span><span class="sxs-lookup"><span data-stu-id="b637f-179">Storage of CLI settings</span></span>
<span data-ttu-id="b637f-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span><span class="sxs-lookup"><span data-stu-id="b637f-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="b637f-181">Your `user` directory is protected by your operating system.</span><span class="sxs-lookup"><span data-stu-id="b637f-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="b637f-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span><span class="sxs-lookup"><span data-stu-id="b637f-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="b637f-183">You can do so in the following ways:</span><span class="sxs-lookup"><span data-stu-id="b637f-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="b637f-184">On Windows, modify the directory properties or use BitLocker.</span><span class="sxs-lookup"><span data-stu-id="b637f-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="b637f-185">On Mac, turn on FileVault for the directory.</span><span class="sxs-lookup"><span data-stu-id="b637f-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="b637f-186">On Ubuntu, use the Encrypted Home directory feature.</span><span class="sxs-lookup"><span data-stu-id="b637f-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="b637f-187">Other Linux distributions offer similar features.</span><span class="sxs-lookup"><span data-stu-id="b637f-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="b637f-188">Logging out</span><span class="sxs-lookup"><span data-stu-id="b637f-188">Logging out</span></span>
<span data-ttu-id="b637f-189">To log out, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b637f-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="b637f-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span><span class="sxs-lookup"><span data-stu-id="b637f-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="b637f-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span><span class="sxs-lookup"><span data-stu-id="b637f-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b637f-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="b637f-192">Next steps</span></span>
* <span data-ttu-id="b637f-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b637f-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="b637f-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b637f-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="b637f-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="b637f-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
