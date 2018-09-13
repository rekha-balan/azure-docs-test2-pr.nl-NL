---
title: Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections
description: Create a web app on Microsoft Azure and connect it to an on-premises SQL Server database
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 17a7ca893641b708d1b32c153914d50d3ae11aff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671128"
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="28e69-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="28e69-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="28e69-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span><span class="sxs-lookup"><span data-stu-id="28e69-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="28e69-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span><span class="sxs-lookup"><span data-stu-id="28e69-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="28e69-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span><span class="sxs-lookup"><span data-stu-id="28e69-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="28e69-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span><span class="sxs-lookup"><span data-stu-id="28e69-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="28e69-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="28e69-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="28e69-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="28e69-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="28e69-110">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="28e69-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="28e69-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="28e69-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="28e69-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="28e69-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="28e69-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="28e69-113">Prerequisites</span></span>
<span data-ttu-id="28e69-114">To complete this tutorial, you'll need the following products.</span><span class="sxs-lookup"><span data-stu-id="28e69-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="28e69-115">All are available in free versions, so you can start developing for Azure entirely for free.</span><span class="sxs-lookup"><span data-stu-id="28e69-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="28e69-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28e69-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="28e69-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="28e69-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="28e69-118">Install this before continuing.</span><span class="sxs-lookup"><span data-stu-id="28e69-118">Install this before continuing.</span></span>
* <span data-ttu-id="28e69-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span><span class="sxs-lookup"><span data-stu-id="28e69-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="28e69-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="28e69-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="28e69-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="28e69-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="28e69-122">Choose the **Express** (not LocalDB) version.</span><span class="sxs-lookup"><span data-stu-id="28e69-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="28e69-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="28e69-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="28e69-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="28e69-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="28e69-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="28e69-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="28e69-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span><span class="sxs-lookup"><span data-stu-id="28e69-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="28e69-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span><span class="sxs-lookup"><span data-stu-id="28e69-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="28e69-128">Notes</span><span class="sxs-lookup"><span data-stu-id="28e69-128">Notes</span></span>
<span data-ttu-id="28e69-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span><span class="sxs-lookup"><span data-stu-id="28e69-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="28e69-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span><span class="sxs-lookup"><span data-stu-id="28e69-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="28e69-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span><span class="sxs-lookup"><span data-stu-id="28e69-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="28e69-132">Must have outbound connectivity to Azure over:</span><span class="sxs-lookup"><span data-stu-id="28e69-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="28e69-133">Port</span><span class="sxs-lookup"><span data-stu-id="28e69-133">Port</span></span> | <span data-ttu-id="28e69-134">Why</span><span class="sxs-lookup"><span data-stu-id="28e69-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="28e69-135">80</span><span class="sxs-lookup"><span data-stu-id="28e69-135">80</span></span> |<span data-ttu-id="28e69-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span><span class="sxs-lookup"><span data-stu-id="28e69-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="28e69-137">443</span><span class="sxs-lookup"><span data-stu-id="28e69-137">443</span></span> |<span data-ttu-id="28e69-138">**Optional** for data connectivity.</span><span class="sxs-lookup"><span data-stu-id="28e69-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="28e69-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span><span class="sxs-lookup"><span data-stu-id="28e69-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="28e69-140">5671 and 9352</span><span class="sxs-lookup"><span data-stu-id="28e69-140">5671 and 9352</span></span> |<span data-ttu-id="28e69-141">**Recommended** but Optional for data connectivity.</span><span class="sxs-lookup"><span data-stu-id="28e69-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="28e69-142">Note this mode usually yields higher throughput.</span><span class="sxs-lookup"><span data-stu-id="28e69-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="28e69-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span><span class="sxs-lookup"><span data-stu-id="28e69-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="28e69-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span><span class="sxs-lookup"><span data-stu-id="28e69-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="28e69-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span><span class="sxs-lookup"><span data-stu-id="28e69-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="28e69-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="28e69-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="28e69-147">A.</span><span class="sxs-lookup"><span data-stu-id="28e69-147">A.</span></span> <span data-ttu-id="28e69-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span><span class="sxs-lookup"><span data-stu-id="28e69-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="28e69-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="28e69-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="28e69-150">Install SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="28e69-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="28e69-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="28e69-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="28e69-152">The SQL Server Installation Center wizard appears.</span><span class="sxs-lookup"><span data-stu-id="28e69-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="28e69-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span><span class="sxs-lookup"><span data-stu-id="28e69-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="28e69-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span><span class="sxs-lookup"><span data-stu-id="28e69-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="28e69-156">On the **Instance Configuration** page, choose **Default instance**.</span><span class="sxs-lookup"><span data-stu-id="28e69-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="28e69-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span><span class="sxs-lookup"><span data-stu-id="28e69-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="28e69-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="28e69-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="28e69-160">Accept the defaults on the **Server Configuration** page.</span><span class="sxs-lookup"><span data-stu-id="28e69-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="28e69-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span><span class="sxs-lookup"><span data-stu-id="28e69-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="28e69-163">In this tutorial, you will be using SQL Server authentication.</span><span class="sxs-lookup"><span data-stu-id="28e69-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="28e69-164">Be sure to remember the password that you provide, because you will need it later.</span><span class="sxs-lookup"><span data-stu-id="28e69-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="28e69-165">Step through the rest of the wizard to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="28e69-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="28e69-166">Enable TCP/IP</span><span class="sxs-lookup"><span data-stu-id="28e69-166">Enable TCP/IP</span></span>
<span data-ttu-id="28e69-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="28e69-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="28e69-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span><span class="sxs-lookup"><span data-stu-id="28e69-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="28e69-169">Create a SQL Server database on-premises</span><span class="sxs-lookup"><span data-stu-id="28e69-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="28e69-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span><span class="sxs-lookup"><span data-stu-id="28e69-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="28e69-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span><span class="sxs-lookup"><span data-stu-id="28e69-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="28e69-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span><span class="sxs-lookup"><span data-stu-id="28e69-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="28e69-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="28e69-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="28e69-174">For **Server type**, choose **Database Engine**.</span><span class="sxs-lookup"><span data-stu-id="28e69-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="28e69-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span><span class="sxs-lookup"><span data-stu-id="28e69-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="28e69-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="28e69-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="28e69-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span><span class="sxs-lookup"><span data-stu-id="28e69-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="28e69-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28e69-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="28e69-181">Note that you do not make any changes to the database at this point.</span><span class="sxs-lookup"><span data-stu-id="28e69-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="28e69-182">The membership information will be added automatically later by your web application when you run it.</span><span class="sxs-lookup"><span data-stu-id="28e69-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="28e69-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span><span class="sxs-lookup"><span data-stu-id="28e69-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="28e69-185">B.</span><span class="sxs-lookup"><span data-stu-id="28e69-185">B.</span></span> <span data-ttu-id="28e69-186">Create a web app in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="28e69-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="28e69-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span><span class="sxs-lookup"><span data-stu-id="28e69-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="28e69-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span><span class="sxs-lookup"><span data-stu-id="28e69-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="28e69-190">Configure your web app, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="28e69-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="28e69-192">After a few moments, the web app is created and its web app blade appears.</span><span class="sxs-lookup"><span data-stu-id="28e69-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="28e69-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span><span class="sxs-lookup"><span data-stu-id="28e69-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="28e69-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span><span class="sxs-lookup"><span data-stu-id="28e69-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="28e69-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span><span class="sxs-lookup"><span data-stu-id="28e69-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="28e69-197">C.</span><span class="sxs-lookup"><span data-stu-id="28e69-197">C.</span></span> <span data-ttu-id="28e69-198">Create a Hybrid Connection and a BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="28e69-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="28e69-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span><span class="sxs-lookup"><span data-stu-id="28e69-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Hybrid connections][CreateHCHCIcon]
2. <span data-ttu-id="28e69-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span><span class="sxs-lookup"><span data-stu-id="28e69-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="28e69-202">On the **Create hybrid connection** blade:</span><span class="sxs-lookup"><span data-stu-id="28e69-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="28e69-203">For **Name**, provide a name for the connection.</span><span class="sxs-lookup"><span data-stu-id="28e69-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="28e69-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span><span class="sxs-lookup"><span data-stu-id="28e69-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="28e69-205">For **Port**, enter 1433 (the default port for SQL Server).</span><span class="sxs-lookup"><span data-stu-id="28e69-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="28e69-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span><span class="sxs-lookup"><span data-stu-id="28e69-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="28e69-208">Click **OK** twice.</span><span class="sxs-lookup"><span data-stu-id="28e69-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="28e69-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span><span class="sxs-lookup"><span data-stu-id="28e69-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="28e69-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span><span class="sxs-lookup"><span data-stu-id="28e69-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="28e69-212">Next, you will create a corresponding on-premises piece.</span><span class="sxs-lookup"><span data-stu-id="28e69-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="28e69-213">D.</span><span class="sxs-lookup"><span data-stu-id="28e69-213">D.</span></span> <span data-ttu-id="28e69-214">Install the on-premises Hybrid Connection Manager to complete the connection</span><span class="sxs-lookup"><span data-stu-id="28e69-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="28e69-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span><span class="sxs-lookup"><span data-stu-id="28e69-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="28e69-216">E.</span><span class="sxs-lookup"><span data-stu-id="28e69-216">E.</span></span> <span data-ttu-id="28e69-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span><span class="sxs-lookup"><span data-stu-id="28e69-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="28e69-218">Create a basic ASP.NET project</span><span class="sxs-lookup"><span data-stu-id="28e69-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="28e69-219">In Visual Studio, on the **File** menu, create a new Project:</span><span class="sxs-lookup"><span data-stu-id="28e69-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="28e69-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28e69-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="28e69-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28e69-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="28e69-225">When the project has been created, the application readme page appears.</span><span class="sxs-lookup"><span data-stu-id="28e69-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="28e69-226">Do not run the web project yet.</span><span class="sxs-lookup"><span data-stu-id="28e69-226">Do not run the web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="28e69-228">Edit the database connection string for the application</span><span class="sxs-lookup"><span data-stu-id="28e69-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="28e69-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span><span class="sxs-lookup"><span data-stu-id="28e69-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="28e69-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span><span class="sxs-lookup"><span data-stu-id="28e69-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="28e69-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span><span class="sxs-lookup"><span data-stu-id="28e69-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="28e69-232">In Solution Explorer, double-click the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="28e69-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="28e69-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span><span class="sxs-lookup"><span data-stu-id="28e69-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Connection string][HCVSConnectionString]
   
    <span data-ttu-id="28e69-236">When composing the connection string, keep in mind the following:</span><span class="sxs-lookup"><span data-stu-id="28e69-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="28e69-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span><span class="sxs-lookup"><span data-stu-id="28e69-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="28e69-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="28e69-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="28e69-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="28e69-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="28e69-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span><span class="sxs-lookup"><span data-stu-id="28e69-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="28e69-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span><span class="sxs-lookup"><span data-stu-id="28e69-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="28e69-242">Click **Save** in Visual Studio to save the Web.config file.</span><span class="sxs-lookup"><span data-stu-id="28e69-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="28e69-243">Run the project locally and register a new user</span><span class="sxs-lookup"><span data-stu-id="28e69-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="28e69-244">Now, run your new web project locally by clicking the browse button under Debug.</span><span class="sxs-lookup"><span data-stu-id="28e69-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="28e69-245">This example uses Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="28e69-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="28e69-247">On the upper right of the default web page, choose **Register** to register a new account:</span><span class="sxs-lookup"><span data-stu-id="28e69-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="28e69-249">Enter a user name and password:</span><span class="sxs-lookup"><span data-stu-id="28e69-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="28e69-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span><span class="sxs-lookup"><span data-stu-id="28e69-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="28e69-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span><span class="sxs-lookup"><span data-stu-id="28e69-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="28e69-253">You will see this table later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="28e69-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="28e69-254">Close the browser window of the default web page.</span><span class="sxs-lookup"><span data-stu-id="28e69-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="28e69-255">This stops the application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="28e69-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="28e69-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span><span class="sxs-lookup"><span data-stu-id="28e69-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="28e69-257">F.</span><span class="sxs-lookup"><span data-stu-id="28e69-257">F.</span></span> <span data-ttu-id="28e69-258">Publish the web application to Azure and test it</span><span class="sxs-lookup"><span data-stu-id="28e69-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="28e69-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span><span class="sxs-lookup"><span data-stu-id="28e69-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="28e69-260">Publish the web application</span><span class="sxs-lookup"><span data-stu-id="28e69-260">Publish the web application</span></span>
1. <span data-ttu-id="28e69-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="28e69-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="28e69-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span><span class="sxs-lookup"><span data-stu-id="28e69-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Download publish profile][PortalDownloadPublishProfile]
   
    <span data-ttu-id="28e69-264">Next, you will import this file into your Visual Studio web application.</span><span class="sxs-lookup"><span data-stu-id="28e69-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="28e69-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="28e69-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="28e69-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span><span class="sxs-lookup"><span data-stu-id="28e69-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Import][HCVSPublishWebDialogImport]
4. <span data-ttu-id="28e69-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28e69-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Browse to profile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="28e69-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span><span class="sxs-lookup"><span data-stu-id="28e69-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Click Publish][HCVSClickPublish]
   
    <span data-ttu-id="28e69-273">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="28e69-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="28e69-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span><span class="sxs-lookup"><span data-stu-id="28e69-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="28e69-275">Next, you will use your live web application to see its Hybrid Connection in action.</span><span class="sxs-lookup"><span data-stu-id="28e69-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="28e69-276">Test the completed web application on Azure</span><span class="sxs-lookup"><span data-stu-id="28e69-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="28e69-277">On the top right of your web page on Azure, choose **Log in**.</span><span class="sxs-lookup"><span data-stu-id="28e69-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="28e69-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span><span class="sxs-lookup"><span data-stu-id="28e69-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="28e69-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span><span class="sxs-lookup"><span data-stu-id="28e69-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="28e69-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span><span class="sxs-lookup"><span data-stu-id="28e69-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="28e69-283">Provide a new user name and password, and then click **Register**.</span><span class="sxs-lookup"><span data-stu-id="28e69-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="28e69-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span><span class="sxs-lookup"><span data-stu-id="28e69-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="28e69-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span><span class="sxs-lookup"><span data-stu-id="28e69-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="28e69-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span><span class="sxs-lookup"><span data-stu-id="28e69-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![View the results][HCTestSSMSTree]
5. <span data-ttu-id="28e69-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="28e69-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="28e69-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span><span class="sxs-lookup"><span data-stu-id="28e69-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="28e69-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="28e69-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="28e69-293">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="28e69-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="28e69-294">See Also</span><span class="sxs-lookup"><span data-stu-id="28e69-294">See Also</span></span>
[<span data-ttu-id="28e69-295">Hybrid Connections overview</span><span class="sxs-lookup"><span data-stu-id="28e69-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="28e69-296">Josh Twist introduces hybrid connections (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="28e69-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="28e69-297">Hybrid Connections overview</span><span class="sxs-lookup"><span data-stu-id="28e69-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="28e69-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span><span class="sxs-lookup"><span data-stu-id="28e69-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="28e69-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span><span class="sxs-lookup"><span data-stu-id="28e69-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="28e69-300">Access on-premises resources using hybrid connections in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="28e69-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="28e69-301">ASP.NET Identity Overview</span><span class="sxs-lookup"><span data-stu-id="28e69-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
































