---
title: Azure Functions Runtime Installation | Microsoft Docs
description: How to Install the Azure Functions Runtime preview 2
services: functions
author: apwestgarth
manager: stefsch
ms.assetid: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 11/28/2017
ms.author: anwestg
ms.openlocfilehash: 1ad1d2c74be97afcb62f3f8e8161111f4938f645
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864473"
---
# <a name="install-the-azure-functions-runtime-preview-2"></a><span data-ttu-id="d08da-103">Install the Azure Functions Runtime preview 2</span><span class="sxs-lookup"><span data-stu-id="d08da-103">Install the Azure Functions Runtime preview 2</span></span>

<span data-ttu-id="d08da-104">If you would like to install the Azure Functions Runtime preview 2, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="d08da-104">If you would like to install the Azure Functions Runtime preview 2, follow these steps:</span></span>

1. <span data-ttu-id="d08da-105">Ensure your machine passes the minimum requirements.</span><span class="sxs-lookup"><span data-stu-id="d08da-105">Ensure your machine passes the minimum requirements.</span></span>
1. <span data-ttu-id="d08da-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafrv2).</span><span class="sxs-lookup"><span data-stu-id="d08da-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafrv2).</span></span>
1. <span data-ttu-id="d08da-107">Uninstall the Azure Functions Runtime preview 1.</span><span class="sxs-lookup"><span data-stu-id="d08da-107">Uninstall the Azure Functions Runtime preview 1.</span></span>
1. <span data-ttu-id="d08da-108">Install the Azure Functions Runtime preview 2.</span><span class="sxs-lookup"><span data-stu-id="d08da-108">Install the Azure Functions Runtime preview 2.</span></span>
1. <span data-ttu-id="d08da-109">Complete the configuration of the Azure Functions Runtime preview 2.</span><span class="sxs-lookup"><span data-stu-id="d08da-109">Complete the configuration of the Azure Functions Runtime preview 2.</span></span>
1. <span data-ttu-id="d08da-110">Create your first function in Azure Functions Runtime Preview</span><span class="sxs-lookup"><span data-stu-id="d08da-110">Create your first function in Azure Functions Runtime Preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08da-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d08da-111">Prerequisites</span></span>

<span data-ttu-id="d08da-112">Before you install the Azure Functions Runtime preview, you must have the following resources available:</span><span class="sxs-lookup"><span data-stu-id="d08da-112">Before you install the Azure Functions Runtime preview, you must have the following resources available:</span></span>

1. <span data-ttu-id="d08da-113">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="d08da-113">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="d08da-114">A SQL Server instance running within your network.</span><span class="sxs-lookup"><span data-stu-id="d08da-114">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="d08da-115">Minimum edition required is SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="d08da-115">Minimum edition required is SQL Server Express.</span></span>

## <a name="uninstall-previous-version"></a><span data-ttu-id="d08da-116">Uninstall Previous Version</span><span class="sxs-lookup"><span data-stu-id="d08da-116">Uninstall Previous Version</span></span>

<span data-ttu-id="d08da-117">If you have previously installed the Azure Functions Runtime preview, you must uninstall before installing the latest release.</span><span class="sxs-lookup"><span data-stu-id="d08da-117">If you have previously installed the Azure Functions Runtime preview, you must uninstall before installing the latest release.</span></span>  <span data-ttu-id="d08da-118">Uninstall the Azure Functions Runtime preview by removing the program in Add/Remove Programs in Windows.</span><span class="sxs-lookup"><span data-stu-id="d08da-118">Uninstall the Azure Functions Runtime preview by removing the program in Add/Remove Programs in Windows.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="d08da-119">Install the Azure Functions Runtime Preview</span><span class="sxs-lookup"><span data-stu-id="d08da-119">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="d08da-120">The Azure Functions Runtime Preview Installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span><span class="sxs-lookup"><span data-stu-id="d08da-120">The Azure Functions Runtime Preview Installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="d08da-121">It is possible to install the Management and Worker role on the same machine.</span><span class="sxs-lookup"><span data-stu-id="d08da-121">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="d08da-122">However, as you add more function apps, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span><span class="sxs-lookup"><span data-stu-id="d08da-122">However, as you add more function apps, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="d08da-123">Install the Management and Worker Role on the same machine</span><span class="sxs-lookup"><span data-stu-id="d08da-123">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="d08da-124">Run the Azure Functions Runtime Preview Installer.</span><span class="sxs-lookup"><span data-stu-id="d08da-124">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Azure Functions Runtime preview installer][1]

1. <span data-ttu-id="d08da-126">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d08da-126">Click **Next**.</span></span>
1. <span data-ttu-id="d08da-127">Once you have read the terms of the **EULA**, **check the box** to accept the terms and click **Next** to advance.</span><span class="sxs-lookup"><span data-stu-id="d08da-127">Once you have read the terms of the **EULA**, **check the box** to accept the terms and click **Next** to advance.</span></span>
1. <span data-ttu-id="d08da-128">Select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d08da-128">Select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and click **Next**.</span></span>

    ![Azure Functions Runtime preview installer - role selection][3]

    > [!NOTE]
    > <span data-ttu-id="d08da-130">You can install the **Functions Worker Role** on many other machines.</span><span class="sxs-lookup"><span data-stu-id="d08da-130">You can install the **Functions Worker Role** on many other machines.</span></span> <span data-ttu-id="d08da-131">To do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span><span class="sxs-lookup"><span data-stu-id="d08da-131">To do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="d08da-132">Click **Next** to have the **Azure Functions Runtime Setup Wizard** begin the installation process on your machine.</span><span class="sxs-lookup"><span data-stu-id="d08da-132">Click **Next** to have the **Azure Functions Runtime Setup Wizard** begin the installation process on your machine.</span></span>
1. <span data-ttu-id="d08da-133">Once complete, the setup wizard launches the **Azure Functions Runtime** configuration tool.</span><span class="sxs-lookup"><span data-stu-id="d08da-133">Once complete, the setup wizard launches the **Azure Functions Runtime** configuration tool.</span></span>

    ![Azure Functions Runtime preview installer complete][6]

    > [!NOTE]
    > <span data-ttu-id="d08da-135">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime Setup** prompts you to reboot your machine to complete the install.</span><span class="sxs-lookup"><span data-stu-id="d08da-135">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime Setup** prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="d08da-136">Configure the Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="d08da-136">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="d08da-137">To complete the Azure Functions Runtime installation, you must complete the configuration.</span><span class="sxs-lookup"><span data-stu-id="d08da-137">To complete the Azure Functions Runtime installation, you must complete the configuration.</span></span>

1. <span data-ttu-id="d08da-138">The **Azure Functions Runtime** configuration tool shows which roles are installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="d08da-138">The **Azure Functions Runtime** configuration tool shows which roles are installed on your machine.</span></span>

    ![Azure Functions Runtime preview configuration tool][7]

1. <span data-ttu-id="d08da-140">Click the **Database** tab, enter the connection details for your SQL Server instance, including specifying a [Database master key](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine), and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="d08da-140">Click the **Database** tab, enter the connection details for your SQL Server instance, including specifying a [Database master key](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine), and click **Apply**.</span></span>  <span data-ttu-id="d08da-141">Connectivity to a SQL Server instance is required in order for the Azure Functions Runtime to create a database to support the Runtime.</span><span class="sxs-lookup"><span data-stu-id="d08da-141">Connectivity to a SQL Server instance is required in order for the Azure Functions Runtime to create a database to support the Runtime.</span></span>

    ![Azure Functions Runtime preview database configuration][8]

1. <span data-ttu-id="d08da-143">Click the **Credentials** tab.  Here, you must create two new credentials for use with a file share for hosting all your function apps.</span><span class="sxs-lookup"><span data-stu-id="d08da-143">Click the **Credentials** tab.  Here, you must create two new credentials for use with a file share for hosting all your function apps.</span></span>  <span data-ttu-id="d08da-144">Specify **User name** and **Password** combinations for the **file share owner** and for the **file share user**, then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="d08da-144">Specify **User name** and **Password** combinations for the **file share owner** and for the **file share user**, then click **Apply**.</span></span>

    ![Azure Functions Runtime preview credentials][9]

1. <span data-ttu-id="d08da-146">Click the **File Share** tab.  Here you must specify the details of the file share  location.</span><span class="sxs-lookup"><span data-stu-id="d08da-146">Click the **File Share** tab.  Here you must specify the details of the file share  location.</span></span>  <span data-ttu-id="d08da-147">The file share can be created for you or you can use an existing File Share and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="d08da-147">The file share can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="d08da-148">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="d08da-148">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>

    ![Azure Functions Runtime preview file share][10]

1. <span data-ttu-id="d08da-150">Click the **IIS** tab.  This tab shows the details of the websites in IIS that the Azure Functions Runtime configuration tool creates.</span><span class="sxs-lookup"><span data-stu-id="d08da-150">Click the **IIS** tab.  This tab shows the details of the websites in IIS that the Azure Functions Runtime configuration tool creates.</span></span>  <span data-ttu-id="d08da-151">You may specify a custom DNS name here for the Azure Functions Runtime preview portal.</span><span class="sxs-lookup"><span data-stu-id="d08da-151">You may specify a custom DNS name here for the Azure Functions Runtime preview portal.</span></span>  <span data-ttu-id="d08da-152">Click **Apply** to complete.</span><span class="sxs-lookup"><span data-stu-id="d08da-152">Click **Apply** to complete.</span></span>

    ![Azure Functions Runtime preview IIS][11]

1. <span data-ttu-id="d08da-154">Click the **Services** tab.  This tab shows the status of the services in your Azure Functions Runtime configuration tool.</span><span class="sxs-lookup"><span data-stu-id="d08da-154">Click the **Services** tab.  This tab shows the status of the services in your Azure Functions Runtime configuration tool.</span></span>  <span data-ttu-id="d08da-155">If the  **Azure Functions Host Activation Service** is not running after initial configuration, click **Start Service**.</span><span class="sxs-lookup"><span data-stu-id="d08da-155">If the  **Azure Functions Host Activation Service** is not running after initial configuration, click **Start Service**.</span></span>

    ![Azure Functions Runtime preview configuration complete][12]

1. <span data-ttu-id="d08da-157">Browse to the **Azure Functions Runtime Portal** as `https://<machinename>.<domain>/`.</span><span class="sxs-lookup"><span data-stu-id="d08da-157">Browse to the **Azure Functions Runtime Portal** as `https://<machinename>.<domain>/`.</span></span>

    ![Azure Functions Runtime preview portal][13]

## <a name="create-your-first-function-in-azure-functions-runtime-preview"></a><span data-ttu-id="d08da-159">Create your first function in Azure Functions Runtime preview</span><span class="sxs-lookup"><span data-stu-id="d08da-159">Create your first function in Azure Functions Runtime preview</span></span>

<span data-ttu-id="d08da-160">To create your first function in Azure Functions Runtime preview</span><span class="sxs-lookup"><span data-stu-id="d08da-160">To create your first function in Azure Functions Runtime preview</span></span>

1. <span data-ttu-id="d08da-161">Browse to the **Azure Functions Runtime Portal** as https://<machinename>.<domain></span><span class="sxs-lookup"><span data-stu-id="d08da-161">Browse to the **Azure Functions Runtime Portal** as https://<machinename>.<domain></span></span> <span data-ttu-id="d08da-162">for example https://mycomputer.mydomain.com</span><span class="sxs-lookup"><span data-stu-id="d08da-162">for example https://mycomputer.mydomain.com</span></span>
1. <span data-ttu-id="d08da-163">You are prompted to **Log in**, if deployed in a domain use your domain account username and password, otherwise use your local account username and password to log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="d08da-163">You are prompted to **Log in**, if deployed in a domain use your domain account username and password, otherwise use your local account username and password to log in to the portal.</span></span>

![Azure Functions Runtime preview portal login][14]

1. <span data-ttu-id="d08da-165">To create function apps, you must create a Subscription.</span><span class="sxs-lookup"><span data-stu-id="d08da-165">To create function apps, you must create a Subscription.</span></span>  <span data-ttu-id="d08da-166">In the top left-hand corner of the portal, click the **+** option next to the subscriptions</span><span class="sxs-lookup"><span data-stu-id="d08da-166">In the top left-hand corner of the portal, click the **+** option next to the subscriptions</span></span>

![Azure Functions Runtime preview portal subscriptions][15]

1. <span data-ttu-id="d08da-168">Choose **DefaultPlan**, enter a name for your Subscription, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d08da-168">Choose **DefaultPlan**, enter a name for your Subscription, and click **Create**.</span></span>

![Azure Functions Runtime preview portal subscription plan and name][16]

1. <span data-ttu-id="d08da-170">All of your function apps are listed in the left-hand pane of the portal.</span><span class="sxs-lookup"><span data-stu-id="d08da-170">All of your function apps are listed in the left-hand pane of the portal.</span></span>  <span data-ttu-id="d08da-171">To create a new Function App, select the heading **Function Apps** and click the **+** option.</span><span class="sxs-lookup"><span data-stu-id="d08da-171">To create a new Function App, select the heading **Function Apps** and click the **+** option.</span></span>

1. <span data-ttu-id="d08da-172">Enter a name for your function app, select the correct Subscription, choose which version of the Azure Functions runtime you wish to program against and click **Create**</span><span class="sxs-lookup"><span data-stu-id="d08da-172">Enter a name for your function app, select the correct Subscription, choose which version of the Azure Functions runtime you wish to program against and click **Create**</span></span>

![Azure Functions Runtime preview portal new function app][17]

1. <span data-ttu-id="d08da-174">Your new function app is listed in the left-hand pane of the portal.</span><span class="sxs-lookup"><span data-stu-id="d08da-174">Your new function app is listed in the left-hand pane of the portal.</span></span>  <span data-ttu-id="d08da-175">Select Functions and then click **New Function** at the top of the center pane in the portal.</span><span class="sxs-lookup"><span data-stu-id="d08da-175">Select Functions and then click **New Function** at the top of the center pane in the portal.</span></span>

![Azure Functions Runtime preview templates][18]

1. <span data-ttu-id="d08da-177">Select the Timer Trigger function, in the right-hand flyout name your function and change the Schedule to `*/5 * * * * *` (this cron expression causes your timer function to execute every five seconds), and click **Create**</span><span class="sxs-lookup"><span data-stu-id="d08da-177">Select the Timer Trigger function, in the right-hand flyout name your function and change the Schedule to `*/5 * * * * *` (this cron expression causes your timer function to execute every five seconds), and click **Create**</span></span>

![Azure Functions Runtime preview new timer function configuration][19]

1. <span data-ttu-id="d08da-179">Your function has now been created.</span><span class="sxs-lookup"><span data-stu-id="d08da-179">Your function has now been created.</span></span>  <span data-ttu-id="d08da-180">You can view the execution log of your Function app by expanding the **log** pane at the bottom of the portal.</span><span class="sxs-lookup"><span data-stu-id="d08da-180">You can view the execution log of your Function app by expanding the **log** pane at the bottom of the portal.</span></span>

![Azure Functions Runtime preview function executing][20]

<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-Progress.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer6-InstallComplete.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[13]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png
[14]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal_Login.png
[15]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal_Subscriptions.png
[16]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal_Subscriptions1.png
[17]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal_NewFunctionApp.png
[18]: ./media/functions-runtime-install/AzureFunctionsRuntime_v1FunctionsTemplates.png
[19]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal_NewTimerFunction.png
[20]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal_RunningV2Function.png
