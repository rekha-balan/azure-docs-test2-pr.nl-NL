---
title: Continuous delivery for cloud services with TFS in Azure | Microsoft Docs
description: Learn how to set up continuous delivery for Azure cloud apps. Code samples for MSBuild command-line statements and PowerShell scripts.
services: cloud-services
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: cc449c4c9f1f040c333cd2c0a811a80f38038a4f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540685"
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a><span data-ttu-id="07c2e-104">Continuous Delivery for Cloud Services in Azure</span><span class="sxs-lookup"><span data-stu-id="07c2e-104">Continuous Delivery for Cloud Services in Azure</span></span>
<span data-ttu-id="07c2e-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span><span class="sxs-lookup"><span data-stu-id="07c2e-105">The process described in this article shows you how to set up continuous delivery for Azure cloud apps.</span></span> <span data-ttu-id="07c2e-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span><span class="sxs-lookup"><span data-stu-id="07c2e-106">This process enables you to automatically create packages and deploy the package to Azure after every code check-in.</span></span> <span data-ttu-id="07c2e-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07c2e-107">The package build process described in this article is equivalent to the **Package** command in Visual Studio, and the publishing steps are equivalent to the **Publish** command in Visual Studio.</span></span>
<span data-ttu-id="07c2e-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="07c2e-108">The article covers the methods you would use to create a build server with MSBuild command-line statements and Windows PowerShell scripts, and it also demonstrates how to optionally configure Visual Studio Team Foundation Server - Team Build definitions to use the MSBuild commands and PowerShell scripts.</span></span> <span data-ttu-id="07c2e-109">The process is customizable for your build environment and Azure target environments.</span><span class="sxs-lookup"><span data-stu-id="07c2e-109">The process is customizable for your build environment and Azure target environments.</span></span>

<span data-ttu-id="07c2e-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span><span class="sxs-lookup"><span data-stu-id="07c2e-110">You can also use Visual Studio Team Services, a version of TFS that is hosted in Azure, to do this more easily.</span></span> <span data-ttu-id="07c2e-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][Continuous Delivery to Azure by Using Visual Studio Team Services] .</span><span class="sxs-lookup"><span data-stu-id="07c2e-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][Continuous Delivery to Azure by Using Visual Studio Team Services] .</span></span>

<span data-ttu-id="07c2e-112">Before you start, you should publish your application from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07c2e-112">Before you start, you should publish your application from Visual Studio.</span></span>
<span data-ttu-id="07c2e-113">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span><span class="sxs-lookup"><span data-stu-id="07c2e-113">This will ensure that all the resources are available and initialized when you attempt to automate the publication process.</span></span>

## <a name="1-configure-the-build-server"></a><span data-ttu-id="07c2e-114">1: Configure the Build Server</span><span class="sxs-lookup"><span data-stu-id="07c2e-114">1: Configure the Build Server</span></span>
<span data-ttu-id="07c2e-115">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span><span class="sxs-lookup"><span data-stu-id="07c2e-115">Before you can create an Azure package by using MSBuild, you must install the required software and tools on the build server.</span></span>

<span data-ttu-id="07c2e-116">Visual Studio is not required to be installed on the build server.</span><span class="sxs-lookup"><span data-stu-id="07c2e-116">Visual Studio is not required to be installed on the build server.</span></span> <span data-ttu-id="07c2e-117">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span><span class="sxs-lookup"><span data-stu-id="07c2e-117">If you want to use Team Foundation Build Service to manage your build server, follow the instructions in the [Team Foundation Build Service][Team Foundation Build Service] documentation.</span></span>

1. <span data-ttu-id="07c2e-118">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span><span class="sxs-lookup"><span data-stu-id="07c2e-118">On the build server, install the [.NET Framework 4.5.2][.NET Framework 4.5.2], which includes MSBuild.</span></span>
2. <span data-ttu-id="07c2e-119">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span><span class="sxs-lookup"><span data-stu-id="07c2e-119">Install the latest [Azure Authoring Tools for .NET](https://azure.microsoft.com/develop/net/).</span></span>
3. <span data-ttu-id="07c2e-120">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span><span class="sxs-lookup"><span data-stu-id="07c2e-120">Install the [Azure Libraries for .NET](http://go.microsoft.com/fwlink/?LinkId=623519).</span></span>
4. <span data-ttu-id="07c2e-121">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span><span class="sxs-lookup"><span data-stu-id="07c2e-121">Copy the Microsoft.WebApplication.targets file from a Visual Studio installation to the build server.</span></span>

   <span data-ttu-id="07c2e-122">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span><span class="sxs-lookup"><span data-stu-id="07c2e-122">On a computer with Visual Studio installed, this file is located in the directory C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications.</span></span> <span data-ttu-id="07c2e-123">You should copy it to the same directory on the build server.</span><span class="sxs-lookup"><span data-stu-id="07c2e-123">You should copy it to the same directory on the build server.</span></span>
5. <span data-ttu-id="07c2e-124">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="07c2e-124">Install the [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).</span></span>

## <a name="2-build-a-package-using-msbuild-commands"></a><span data-ttu-id="07c2e-125">2: Build a Package using MSBuild Commands</span><span class="sxs-lookup"><span data-stu-id="07c2e-125">2: Build a Package using MSBuild Commands</span></span>
<span data-ttu-id="07c2e-126">This section describes how to construct an MSBuild command that builds an Azure package.</span><span class="sxs-lookup"><span data-stu-id="07c2e-126">This section describes how to construct an MSBuild command that builds an Azure package.</span></span> <span data-ttu-id="07c2e-127">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span><span class="sxs-lookup"><span data-stu-id="07c2e-127">Run this step on the build server to verify that everything is configured correctly and that the MSBuild command does what you want it to do.</span></span> <span data-ttu-id="07c2e-128">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span><span class="sxs-lookup"><span data-stu-id="07c2e-128">You can either add this command line to existing build scripts on the build server, or you can use the command line in a TFS Build Definition, as described in the next section.</span></span> <span data-ttu-id="07c2e-129">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="07c2e-129">For more information about command-line parameters and MSBuild, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>

1. <span data-ttu-id="07c2e-130">If Visual Studio is installed on the build server, locate and choose **Visual Studio Commmand Prompt** in the **Visual Studio Tools** folder in Windows.</span><span class="sxs-lookup"><span data-stu-id="07c2e-130">If Visual Studio is installed on the build server, locate and choose **Visual Studio Commmand Prompt** in the **Visual Studio Tools** folder in Windows.</span></span>

   <span data-ttu-id="07c2e-131">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span><span class="sxs-lookup"><span data-stu-id="07c2e-131">If Visual Studio is not installed on the build server, open a command prompt and make sure that MSBuild.exe is accessible on the path.</span></span> <span data-ttu-id="07c2e-132">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span><span class="sxs-lookup"><span data-stu-id="07c2e-132">MSBuild is installed with the .NET Framework in the path %WINDIR%\\Microsoft.NET\\Framework\\*Version*.</span></span> <span data-ttu-id="07c2e-133">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="07c2e-133">For example, to add MSBuild.exe to the PATH environment variable when you have .NET Framework 4 installed, type the following command at the command prompt:</span></span>

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. <span data-ttu-id="07c2e-134">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span><span class="sxs-lookup"><span data-stu-id="07c2e-134">At the command prompt, navigate to the folder containing the Azure project file that you want to build.</span></span>
3. <span data-ttu-id="07c2e-135">Run MSBuild with the /target:Publish option as in the following example:</span><span class="sxs-lookup"><span data-stu-id="07c2e-135">Run MSBuild with the /target:Publish option as in the following example:</span></span>

       MSBuild /target:Publish

   <span data-ttu-id="07c2e-136">This option can be abbreviated as /t:Publish.</span><span class="sxs-lookup"><span data-stu-id="07c2e-136">This option can be abbreviated as /t:Publish.</span></span> <span data-ttu-id="07c2e-137">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span><span class="sxs-lookup"><span data-stu-id="07c2e-137">The /t:Publish option in MSBuild should not be confused with the Publish commands available in Visual Studio when you have the Azure SDK installed.</span></span> <span data-ttu-id="07c2e-138">The /t:Publish option only builds the Azure packages.</span><span class="sxs-lookup"><span data-stu-id="07c2e-138">The /t:Publish option only builds the Azure packages.</span></span> <span data-ttu-id="07c2e-139">It does not deploy the packages as the Publish commands in Visual Studio do.</span><span class="sxs-lookup"><span data-stu-id="07c2e-139">It does not deploy the packages as the Publish commands in Visual Studio do.</span></span>

   <span data-ttu-id="07c2e-140">Optionally, you can specify the project name as an MSBuild parameter.</span><span class="sxs-lookup"><span data-stu-id="07c2e-140">Optionally, you can specify the project name as an MSBuild parameter.</span></span> <span data-ttu-id="07c2e-141">If not specified, the current directory is used.</span><span class="sxs-lookup"><span data-stu-id="07c2e-141">If not specified, the current directory is used.</span></span> <span data-ttu-id="07c2e-142">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="07c2e-142">For more information about MSBuild command line options, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).</span></span>
4. <span data-ttu-id="07c2e-143">Locate the output.</span><span class="sxs-lookup"><span data-stu-id="07c2e-143">Locate the output.</span></span> <span data-ttu-id="07c2e-144">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span><span class="sxs-lookup"><span data-stu-id="07c2e-144">By default, this command creates a directory in relation to the root folder for the project, such as *ProjectDir*\\bin\\*Configuration*\\app.publish\\.</span></span> <span data-ttu-id="07c2e-145">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span><span class="sxs-lookup"><span data-stu-id="07c2e-145">When you build an Azure project, you generate two files, the package file itself and the accompanying configuration file:</span></span>

   * <span data-ttu-id="07c2e-146">Project.cspkg</span><span class="sxs-lookup"><span data-stu-id="07c2e-146">Project.cspkg</span></span>
   * <span data-ttu-id="07c2e-147">ServiceConfiguration.*TargetProfile*.cscfg</span><span class="sxs-lookup"><span data-stu-id="07c2e-147">ServiceConfiguration.*TargetProfile*.cscfg</span></span>

   <span data-ttu-id="07c2e-148">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span><span class="sxs-lookup"><span data-stu-id="07c2e-148">By default, each Azure project includes one service configuration file (.cscfg file) for local (debugging) builds and another for cloud (staging or production) builds, but you can add or remove service configuration files as needed.</span></span> <span data-ttu-id="07c2e-149">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span><span class="sxs-lookup"><span data-stu-id="07c2e-149">When you build a package within Visual Studio, you will be asked which service configuration file to include alongside the package.</span></span>
5. <span data-ttu-id="07c2e-150">Specify the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="07c2e-150">Specify the service configuration file.</span></span> <span data-ttu-id="07c2e-151">When you build a package by using MSBuild, the local service configuration file is included by default.</span><span class="sxs-lookup"><span data-stu-id="07c2e-151">When you build a package by using MSBuild, the local service configuration file is included by default.</span></span> <span data-ttu-id="07c2e-152">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="07c2e-152">To include a different service configuration file, set the TargetProfile property of the MSBuild command, as in the following example:</span></span>

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. <span data-ttu-id="07c2e-153">Specify the location for the output.</span><span class="sxs-lookup"><span data-stu-id="07c2e-153">Specify the location for the output.</span></span> <span data-ttu-id="07c2e-154">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="07c2e-154">Set the path by using the /p:PublishDir=*Directory*\\ option, including the trailing backslash separator, as in the following example:</span></span>

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   <span data-ttu-id="07c2e-155">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span><span class="sxs-lookup"><span data-stu-id="07c2e-155">Once you've constructed and tested an appropriate MSBuild command line to build your projects and combine them into an Azure package, you can add this command line to your build scripts.</span></span> <span data-ttu-id="07c2e-156">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span><span class="sxs-lookup"><span data-stu-id="07c2e-156">If your build server uses custom scripts, this process will depend on the specifics of your custom build process.</span></span> <span data-ttu-id="07c2e-157">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span><span class="sxs-lookup"><span data-stu-id="07c2e-157">If you are using TFS as a build environment, then you can follow the instructions in the next step to add the Azure package build to your build process.</span></span>

## <a name="3-build-a-package-using-tfs-team-build"></a><span data-ttu-id="07c2e-158">3: Build a Package using TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="07c2e-158">3: Build a Package using TFS Team Build</span></span>
<span data-ttu-id="07c2e-159">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span><span class="sxs-lookup"><span data-stu-id="07c2e-159">If you have Team Foundation Server (TFS) set up as a build controller and the build server set up as a TFS build machine, then you can optionally set up an automated build for your Azure package.</span></span> <span data-ttu-id="07c2e-160">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span><span class="sxs-lookup"><span data-stu-id="07c2e-160">For information on how to set up and use Team Foundation server as a build system, see [Scale out your build system][Scale out your build system].</span></span> <span data-ttu-id="07c2e-161">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span><span class="sxs-lookup"><span data-stu-id="07c2e-161">In particular, the following procedure assumes that you have configured your build server as described in [Deploy and configure a build server][Deploy and configure a build server], and that you have created a team project, created a cloud service project in the team project.</span></span>

<span data-ttu-id="07c2e-162">To configure TFS to build Azure packages, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="07c2e-162">To configure TFS to build Azure packages, perform the following steps:</span></span>

1. <span data-ttu-id="07c2e-163">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span><span class="sxs-lookup"><span data-stu-id="07c2e-163">In Visual Studio on your development computer, on the View menu, choose **Team Explorer**, or choose Ctrl+\\, Ctrl+M.</span></span> <span data-ttu-id="07c2e-164">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span><span class="sxs-lookup"><span data-stu-id="07c2e-164">In the Team Explorer window, expand the **Builds** node or choose the **Builds** page, and choose **New Build Definition**.</span></span>

   ![New Build Definition option][0]
2. <span data-ttu-id="07c2e-166">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span><span class="sxs-lookup"><span data-stu-id="07c2e-166">Choose the **Trigger** tab, and specify the desired conditions for when you want the package to be built.</span></span> <span data-ttu-id="07c2e-167">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span><span class="sxs-lookup"><span data-stu-id="07c2e-167">For example, specify **Continuous Integration** to build the package whenever a source control check-in occurs.</span></span>
3. <span data-ttu-id="07c2e-168">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span><span class="sxs-lookup"><span data-stu-id="07c2e-168">Choose the **Source Settings** tab, and make sure your project folder is listed in the **Source Control Folder** column, and the status is **Active**.</span></span>
4. <span data-ttu-id="07c2e-169">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span><span class="sxs-lookup"><span data-stu-id="07c2e-169">Choose the **Build Defaults** tab, and under Build controller, verify the name of the build server.</span></span>  <span data-ttu-id="07c2e-170">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span><span class="sxs-lookup"><span data-stu-id="07c2e-170">Also, choose the option **Copy build output to the following drop folder** and specify the desired drop location.</span></span>
5. <span data-ttu-id="07c2e-171">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span><span class="sxs-lookup"><span data-stu-id="07c2e-171">Choose the **Process** tab. On the Process tab, choose the default template, under **Build**, choose the project if it is not already selected, and expand the **Advanced** section in the **Build** section of the grid.</span></span>
6. <span data-ttu-id="07c2e-172">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span><span class="sxs-lookup"><span data-stu-id="07c2e-172">Choose **MSBuild Arguments**, and set the appropriate MSBuild command line arguments as described in Step 2 above.</span></span> <span data-ttu-id="07c2e-173">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span><span class="sxs-lookup"><span data-stu-id="07c2e-173">For example, enter **/t:Publish /p:PublishDir=\\\\myserver\\drops\\** to build a package and copy the package files to the location \\\\myserver\\drops\\:</span></span>

   ![MSBuild arguments][2]

   > [!NOTE]
   > <span data-ttu-id="07c2e-175">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span><span class="sxs-lookup"><span data-stu-id="07c2e-175">Copying the files to a public share makes it easier to manually deploy the packages from your development computer.</span></span>
7. <span data-ttu-id="07c2e-176">Test the success of your build step by checking in a change to your project, or queue up a new build.</span><span class="sxs-lookup"><span data-stu-id="07c2e-176">Test the success of your build step by checking in a change to your project, or queue up a new build.</span></span> <span data-ttu-id="07c2e-177">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span><span class="sxs-lookup"><span data-stu-id="07c2e-177">To queue up a new build, in the Team Explorer, right-click **All Build Definitions,** and then choose **Queue New Build**.</span></span>

## <a name="4-publish-a-package-using-a-powershell-script"></a><span data-ttu-id="07c2e-178">4: Publish a Package using a PowerShell Script</span><span class="sxs-lookup"><span data-stu-id="07c2e-178">4: Publish a Package using a PowerShell Script</span></span>
<span data-ttu-id="07c2e-179">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span><span class="sxs-lookup"><span data-stu-id="07c2e-179">This section describes how to construct a Windows PowerShell script that will publish the Cloud app package output to Azure using optional parameters.</span></span> <span data-ttu-id="07c2e-180">This script can be called after the build step in your custom build automation.</span><span class="sxs-lookup"><span data-stu-id="07c2e-180">This script can be called after the build step in your custom build automation.</span></span> <span data-ttu-id="07c2e-181">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span><span class="sxs-lookup"><span data-stu-id="07c2e-181">It can also be called from Process Template workflow activities in Visual Studio TFS Team Build.</span></span>

1. <span data-ttu-id="07c2e-182">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span><span class="sxs-lookup"><span data-stu-id="07c2e-182">Install the [Azure PowerShell cmdlets][Azure PowerShell cmdlets] (v0.6.1 or higher).</span></span>
   <span data-ttu-id="07c2e-183">During the cmdlet setup phase choose to install as a snap-in.</span><span class="sxs-lookup"><span data-stu-id="07c2e-183">During the cmdlet setup phase choose to install as a snap-in.</span></span> <span data-ttu-id="07c2e-184">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span><span class="sxs-lookup"><span data-stu-id="07c2e-184">Note that this officially supported version replaces the older version offered through CodePlex, although the previous versions were numbered 2.x.x.</span></span>
2. <span data-ttu-id="07c2e-185">Start Azure PowerShell using the Start menu or Start page.</span><span class="sxs-lookup"><span data-stu-id="07c2e-185">Start Azure PowerShell using the Start menu or Start page.</span></span> <span data-ttu-id="07c2e-186">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span><span class="sxs-lookup"><span data-stu-id="07c2e-186">If you start in this way, the Azure PowerShell cmdlets will be loaded.</span></span>
3. <span data-ttu-id="07c2e-187">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span><span class="sxs-lookup"><span data-stu-id="07c2e-187">At the PowerShell prompt, verify that the PowerShell cmdlets are loaded by entering the partial command `Get-Azure` and then pressing the Tab key for statement completion.</span></span>

   <span data-ttu-id="07c2e-188">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="07c2e-188">If you press the Tab key repeatedly, you should see various Azure PowerShell commands.</span></span>
4. <span data-ttu-id="07c2e-189">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span><span class="sxs-lookup"><span data-stu-id="07c2e-189">Verify that you can connect to your Azure subscription by importing your subscription information from the .publishsettings file.</span></span>

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   <span data-ttu-id="07c2e-190">Then enter the command</span><span class="sxs-lookup"><span data-stu-id="07c2e-190">Then enter the command</span></span>

   `Get-AzureSubscription`

   <span data-ttu-id="07c2e-191">This shows information about your subscription.</span><span class="sxs-lookup"><span data-stu-id="07c2e-191">This shows information about your subscription.</span></span> <span data-ttu-id="07c2e-192">Verify that everything is correct.</span><span class="sxs-lookup"><span data-stu-id="07c2e-192">Verify that everything is correct.</span></span>
5. <span data-ttu-id="07c2e-193">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span><span class="sxs-lookup"><span data-stu-id="07c2e-193">Save the script template provided at the end of this article to your scripts folder as c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.</span></span>
6. <span data-ttu-id="07c2e-194">Review the parameters section of the script.</span><span class="sxs-lookup"><span data-stu-id="07c2e-194">Review the parameters section of the script.</span></span> <span data-ttu-id="07c2e-195">Add or modify any default values.</span><span class="sxs-lookup"><span data-stu-id="07c2e-195">Add or modify any default values.</span></span> <span data-ttu-id="07c2e-196">These values can always be overridden by passing in explicit parameters.</span><span class="sxs-lookup"><span data-stu-id="07c2e-196">These values can always be overridden by passing in explicit parameters.</span></span>
7. <span data-ttu-id="07c2e-197">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span><span class="sxs-lookup"><span data-stu-id="07c2e-197">Ensure there are valid cloud service and storage accounts created in your subscription that can be targeted by the publish script.</span></span> <span data-ttu-id="07c2e-198">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span><span class="sxs-lookup"><span data-stu-id="07c2e-198">The storage account (blob storage) will be used to upload and temporarily store the deployment package and config file while the deployment is being created.</span></span>

   * <span data-ttu-id="07c2e-199">To create a new cloud service, you can call this script or use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="07c2e-199">To create a new cloud service, you can call this script or use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> <span data-ttu-id="07c2e-200">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span><span class="sxs-lookup"><span data-stu-id="07c2e-200">The cloud service name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span>

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * <span data-ttu-id="07c2e-201">To create a new storage account, you can call this script or use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="07c2e-201">To create a new storage account, you can call this script or use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> <span data-ttu-id="07c2e-202">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span><span class="sxs-lookup"><span data-stu-id="07c2e-202">The storage account name will be used as a prefix in a fully qualified domain name and hence it must be unique.</span></span> <span data-ttu-id="07c2e-203">You can try using the same name as the cloud service.</span><span class="sxs-lookup"><span data-stu-id="07c2e-203">You can try using the same name as the cloud service.</span></span>

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. <span data-ttu-id="07c2e-204">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span><span class="sxs-lookup"><span data-stu-id="07c2e-204">Call the script directly from Azure PowerShell, or wire up this script to your host build automation to occur after the package build.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="07c2e-205">The script will always delete or replace your existing deployments by default if they are detected.</span><span class="sxs-lookup"><span data-stu-id="07c2e-205">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="07c2e-206">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span><span class="sxs-lookup"><span data-stu-id="07c2e-206">This is necessary to enable continuous delivery from automation where no user prompting is possible.</span></span>
   >
   >

   <span data-ttu-id="07c2e-207">**Example scenario 1:** continuous deployment to the staging environment of a service:</span><span class="sxs-lookup"><span data-stu-id="07c2e-207">**Example scenario 1:** continuous deployment to the staging environment of a service:</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="07c2e-208">This is typically followed up by test run verification and a VIP swap.</span><span class="sxs-lookup"><span data-stu-id="07c2e-208">This is typically followed up by test run verification and a VIP swap.</span></span> <span data-ttu-id="07c2e-209">The VIP swap can be done via the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) or by using the Move-Deployment cmdlet.</span><span class="sxs-lookup"><span data-stu-id="07c2e-209">The VIP swap can be done via the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) or by using the Move-Deployment cmdlet.</span></span>

   <span data-ttu-id="07c2e-210">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span><span class="sxs-lookup"><span data-stu-id="07c2e-210">**Example scenario 2:** continuous deployment to the production environment of a dedicated test service</span></span>

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   <span data-ttu-id="07c2e-211">**Remote Desktop:**</span><span class="sxs-lookup"><span data-stu-id="07c2e-211">**Remote Desktop:**</span></span>

   <span data-ttu-id="07c2e-212">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span><span class="sxs-lookup"><span data-stu-id="07c2e-212">If Remote Desktop is enabled in your Azure project you will need to perform additional one-time steps to ensure the correct Cloud Service Certificate is uploaded to all cloud services targeted by this script.</span></span>

   <span data-ttu-id="07c2e-213">Locate the certificate thumbprint values expected by your roles.</span><span class="sxs-lookup"><span data-stu-id="07c2e-213">Locate the certificate thumbprint values expected by your roles.</span></span> <span data-ttu-id="07c2e-214">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span><span class="sxs-lookup"><span data-stu-id="07c2e-214">The thumbprint values are visible in the Certificates section of the cloud config file (i.e. ServiceConfiguration.Cloud.cscfg).</span></span> <span data-ttu-id="07c2e-215">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span><span class="sxs-lookup"><span data-stu-id="07c2e-215">It is also visible in the Remote Desktop Configuration dialog in Visual Studio when you Show Options and view the selected certificate.</span></span>

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   <span data-ttu-id="07c2e-216">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span><span class="sxs-lookup"><span data-stu-id="07c2e-216">Upload Remote Desktop certificates as a one-time setup step using the following cmdlet script:</span></span>

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   <span data-ttu-id="07c2e-217">For example:</span><span class="sxs-lookup"><span data-stu-id="07c2e-217">For example:</span></span>

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   <span data-ttu-id="07c2e-218">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="07c2e-218">Alternatively you can export the certificate file PFX with private key and upload certificates to each target cloud service using the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   <span data-ttu-id="07c2e-219">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span><span class="sxs-lookup"><span data-stu-id="07c2e-219">**Upgrade Deployment vs. Delete Deployment -\> New Deployment**</span></span>

   <span data-ttu-id="07c2e-220">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span><span class="sxs-lookup"><span data-stu-id="07c2e-220">The script will by default perform an Upgrade Deployment ($enableDeploymentUpgrade = 1) when no parameter is passed in or the value 1 is passed explicitly.</span></span> <span data-ttu-id="07c2e-221">For single instances this has the advantage of taking less time than a full deployment.</span><span class="sxs-lookup"><span data-stu-id="07c2e-221">For single instances this has the advantage of taking less time than a full deployment.</span></span> <span data-ttu-id="07c2e-222">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span><span class="sxs-lookup"><span data-stu-id="07c2e-222">For instances that require high availability this also has the advantage of leaving some instances running while others are upgraded (walking your update domain), plus your VIP will not be deleted.</span></span>

   <span data-ttu-id="07c2e-223">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span><span class="sxs-lookup"><span data-stu-id="07c2e-223">Upgrade Deployment can be disabled in the script ($enableDeploymentUpgrade = 0) or by passing *-enableDeploymentUpgrade 0* as a parameter, which alters the script behavior to first delete any existing deployment and then create a new deployment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="07c2e-224">The script will always delete or replace your existing deployments by default if they are detected.</span><span class="sxs-lookup"><span data-stu-id="07c2e-224">The script will always delete or replace your existing deployments by default if they are detected.</span></span> <span data-ttu-id="07c2e-225">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span><span class="sxs-lookup"><span data-stu-id="07c2e-225">This is necessary to enable continuous delivery from automation where no user/operator prompting is possible.</span></span>
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a><span data-ttu-id="07c2e-226">5: Publish a Package using TFS Team Build</span><span class="sxs-lookup"><span data-stu-id="07c2e-226">5: Publish a Package using TFS Team Build</span></span>
<span data-ttu-id="07c2e-227">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span><span class="sxs-lookup"><span data-stu-id="07c2e-227">This optional step connects TFS Team Build to the script created in step 4, which handles publishing of the package build to Azure.</span></span> <span data-ttu-id="07c2e-228">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span><span class="sxs-lookup"><span data-stu-id="07c2e-228">This entails modifying the Process Template used by your build definition so that it runs a Publish activity at the end of the workflow.</span></span> <span data-ttu-id="07c2e-229">The Publish activity will execute your PowerShell command passing in parameters from the build.</span><span class="sxs-lookup"><span data-stu-id="07c2e-229">The Publish activity will execute your PowerShell command passing in parameters from the build.</span></span> <span data-ttu-id="07c2e-230">Output of the MSBuild targets and publish script will be piped into the standard build output.</span><span class="sxs-lookup"><span data-stu-id="07c2e-230">Output of the MSBuild targets and publish script will be piped into the standard build output.</span></span>

1. <span data-ttu-id="07c2e-231">Edit the Build Definition responsible for continuous deploy.</span><span class="sxs-lookup"><span data-stu-id="07c2e-231">Edit the Build Definition responsible for continuous deploy.</span></span>
2. <span data-ttu-id="07c2e-232">Select the **Process** tab.</span><span class="sxs-lookup"><span data-stu-id="07c2e-232">Select the **Process** tab.</span></span>
3. <span data-ttu-id="07c2e-233">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span><span class="sxs-lookup"><span data-stu-id="07c2e-233">Follow [these instructions](http://msdn.microsoft.com/library/dd647551.aspx) to add an Activity project for the build process template, download the default template, add it to the project and check it in.</span></span> <span data-ttu-id="07c2e-234">Give the build process template a new name, such as AzureBuildProcessTemplate.</span><span class="sxs-lookup"><span data-stu-id="07c2e-234">Give the build process template a new name, such as AzureBuildProcessTemplate.</span></span>
4. <span data-ttu-id="07c2e-235">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span><span class="sxs-lookup"><span data-stu-id="07c2e-235">Return to the **Process** tab, and use **Show Details** to show a list of available build process templates.</span></span> <span data-ttu-id="07c2e-236">Choose the **New...** button, and navigate to the project you just added and checked in.</span><span class="sxs-lookup"><span data-stu-id="07c2e-236">Choose the **New...** button, and navigate to the project you just added and checked in.</span></span> <span data-ttu-id="07c2e-237">Locate the template you just created and choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="07c2e-237">Locate the template you just created and choose **OK**.</span></span>
5. <span data-ttu-id="07c2e-238">Open the selected Process Template for editing.</span><span class="sxs-lookup"><span data-stu-id="07c2e-238">Open the selected Process Template for editing.</span></span> <span data-ttu-id="07c2e-239">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span><span class="sxs-lookup"><span data-stu-id="07c2e-239">You can open directly in the Workflow designer or in the XML editor to work with the XAML.</span></span>
6. <span data-ttu-id="07c2e-240">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span><span class="sxs-lookup"><span data-stu-id="07c2e-240">Add the following list of new arguments as separate line items in the arguments tab of the workflow designer.</span></span> <span data-ttu-id="07c2e-241">All arguments should have direction=In and type=String.</span><span class="sxs-lookup"><span data-stu-id="07c2e-241">All arguments should have direction=In and type=String.</span></span> <span data-ttu-id="07c2e-242">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span><span class="sxs-lookup"><span data-stu-id="07c2e-242">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![List of arguments][3]

   <span data-ttu-id="07c2e-244">The corresponding XAML looks like this:</span><span class="sxs-lookup"><span data-stu-id="07c2e-244">The corresponding XAML looks like this:</span></span>

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. <span data-ttu-id="07c2e-245">Add a new sequence at the end of Run On Agent:</span><span class="sxs-lookup"><span data-stu-id="07c2e-245">Add a new sequence at the end of Run On Agent:</span></span>

   1. <span data-ttu-id="07c2e-246">Start by adding an If Statement activity to check for a valid script file.</span><span class="sxs-lookup"><span data-stu-id="07c2e-246">Start by adding an If Statement activity to check for a valid script file.</span></span> <span data-ttu-id="07c2e-247">Set the condition to this value:</span><span class="sxs-lookup"><span data-stu-id="07c2e-247">Set the condition to this value:</span></span>

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. <span data-ttu-id="07c2e-248">In the Then case of the If Statement, add a new Sequence activity.</span><span class="sxs-lookup"><span data-stu-id="07c2e-248">In the Then case of the If Statement, add a new Sequence activity.</span></span> <span data-ttu-id="07c2e-249">Set the display name to 'Start publish'</span><span class="sxs-lookup"><span data-stu-id="07c2e-249">Set the display name to 'Start publish'</span></span>
   3. <span data-ttu-id="07c2e-250">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span><span class="sxs-lookup"><span data-stu-id="07c2e-250">With the Start publish sequence still selected, add the following list of new variables as separate line items in the variables tab of the workflow designer.</span></span> <span data-ttu-id="07c2e-251">All variables should have Variable type =String and Scope=Start publish.</span><span class="sxs-lookup"><span data-stu-id="07c2e-251">All variables should have Variable type =String and Scope=Start publish.</span></span> <span data-ttu-id="07c2e-252">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span><span class="sxs-lookup"><span data-stu-id="07c2e-252">These will be used to flow parameters from the build definition into the workflow, which then get used to call the publish script.</span></span>

      * <span data-ttu-id="07c2e-253">SubscriptionDataFilePath, of type String</span><span class="sxs-lookup"><span data-stu-id="07c2e-253">SubscriptionDataFilePath, of type String</span></span>
      * <span data-ttu-id="07c2e-254">PublishScriptFilePath, of type String</span><span class="sxs-lookup"><span data-stu-id="07c2e-254">PublishScriptFilePath, of type String</span></span>

        ![New variables][4]
   4. <span data-ttu-id="07c2e-256">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span><span class="sxs-lookup"><span data-stu-id="07c2e-256">If you are using TFS 2012 or earlier, add a ConvertWorkspaceItem activity at the beginning of the new Sequence.</span></span> <span data-ttu-id="07c2e-257">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span><span class="sxs-lookup"><span data-stu-id="07c2e-257">If you are using TFS 2013 or later, add a GetLocalPath activity at the beginning of the new sequence.</span></span> <span data-ttu-id="07c2e-258">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-258">For a ConvertWorkspaceItem, set the properties as follows: Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="07c2e-259">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-259">For a GetLocalPath activity, set the property IncomingPath to 'PublishScriptLocation', and the Result to 'PublishScriptFilePath'.</span></span> <span data-ttu-id="07c2e-260">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span><span class="sxs-lookup"><span data-stu-id="07c2e-260">This activity converts the path to the publish script from TFS server locations (if applicable) to a standard local disk path.</span></span>
   5. <span data-ttu-id="07c2e-261">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span><span class="sxs-lookup"><span data-stu-id="07c2e-261">If you are using TFS 2012 or earlier, add another ConvertWorkspaceItem activity at the end of the new Sequence.</span></span> <span data-ttu-id="07c2e-262">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-262">Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'.</span></span> <span data-ttu-id="07c2e-263">If you are using TFS 2013 or later, add another GetLocalPath.</span><span class="sxs-lookup"><span data-stu-id="07c2e-263">If you are using TFS 2013 or later, add another GetLocalPath.</span></span> <span data-ttu-id="07c2e-264">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span><span class="sxs-lookup"><span data-stu-id="07c2e-264">IncomingPath='SubscriptionDataFileLocation', and Result='SubscriptionDataFilePath.'</span></span>
   6. <span data-ttu-id="07c2e-265">Add an InvokeProcess activity at the end of the new Sequence.</span><span class="sxs-lookup"><span data-stu-id="07c2e-265">Add an InvokeProcess activity at the end of the new Sequence.</span></span>
      <span data-ttu-id="07c2e-266">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span><span class="sxs-lookup"><span data-stu-id="07c2e-266">This activity calls PowerShell.exe with the arguments passed in by the Build Definition.</span></span>

      + <span data-ttu-id="07c2e-267">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span><span class="sxs-lookup"><span data-stu-id="07c2e-267">Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)</span></span>
      + <span data-ttu-id="07c2e-268">DisplayName = Execute publish script</span><span class="sxs-lookup"><span data-stu-id="07c2e-268">DisplayName = Execute publish script</span></span>
      + <span data-ttu-id="07c2e-269">FileName = "PowerShell" (include the quotes)</span><span class="sxs-lookup"><span data-stu-id="07c2e-269">FileName = "PowerShell" (include the quotes)</span></span>
      + <span data-ttu-id="07c2e-270">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span><span class="sxs-lookup"><span data-stu-id="07c2e-270">OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)</span></span>
   7. <span data-ttu-id="07c2e-271">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-271">In the **Handle Standard Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="07c2e-272">This is a variable to store the standard output data.</span><span class="sxs-lookup"><span data-stu-id="07c2e-272">This is a variable to store the standard output data.</span></span>
   8. <span data-ttu-id="07c2e-273">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span><span class="sxs-lookup"><span data-stu-id="07c2e-273">Add a WriteBuildMessage activity just below the **Handle Standard Output** section.</span></span> <span data-ttu-id="07c2e-274">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-274">Set the Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' and the Message='data'.</span></span> <span data-ttu-id="07c2e-275">This ensures the standard output of the script will get written to the build output.</span><span class="sxs-lookup"><span data-stu-id="07c2e-275">This ensures the standard output of the script will get written to the build output.</span></span>
   9. <span data-ttu-id="07c2e-276">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-276">In the **Handle Error Output** section textbox of the InvokeProcess, set the textbox value to 'data'.</span></span> <span data-ttu-id="07c2e-277">This is a variable to store the standard error data.</span><span class="sxs-lookup"><span data-stu-id="07c2e-277">This is a variable to store the standard error data.</span></span>
   10. <span data-ttu-id="07c2e-278">Add a WriteBuildError activity just below the **Handle Error Output** section.</span><span class="sxs-lookup"><span data-stu-id="07c2e-278">Add a WriteBuildError activity just below the **Handle Error Output** section.</span></span> <span data-ttu-id="07c2e-279">Set the Message='data'.</span><span class="sxs-lookup"><span data-stu-id="07c2e-279">Set the Message='data'.</span></span> <span data-ttu-id="07c2e-280">This ensures the standard errors of the script will get written to the build error output.</span><span class="sxs-lookup"><span data-stu-id="07c2e-280">This ensures the standard errors of the script will get written to the build error output.</span></span>
   11. <span data-ttu-id="07c2e-281">Correct any errors, indicated by blue exclamation marks.</span><span class="sxs-lookup"><span data-stu-id="07c2e-281">Correct any errors, indicated by blue exclamation marks.</span></span> <span data-ttu-id="07c2e-282">Hover over the exclamation marks to get a hint about the error.</span><span class="sxs-lookup"><span data-stu-id="07c2e-282">Hover over the exclamation marks to get a hint about the error.</span></span> <span data-ttu-id="07c2e-283">Save the workflow to clear errors.</span><span class="sxs-lookup"><span data-stu-id="07c2e-283">Save the workflow to clear errors.</span></span>

   <span data-ttu-id="07c2e-284">The final result of the publish workflow activities will look like this in the designer:</span><span class="sxs-lookup"><span data-stu-id="07c2e-284">The final result of the publish workflow activities will look like this in the designer:</span></span>

   ![Workflow activities][5]

   <span data-ttu-id="07c2e-286">The final result of the publish workflow activities will look like this in XAML:</span><span class="sxs-lookup"><span data-stu-id="07c2e-286">The final result of the publish workflow activities will look like this in XAML:</span></span>

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. <span data-ttu-id="07c2e-287">Save the build process template workflow and Check In this file.</span><span class="sxs-lookup"><span data-stu-id="07c2e-287">Save the build process template workflow and Check In this file.</span></span>
9. <span data-ttu-id="07c2e-288">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span><span class="sxs-lookup"><span data-stu-id="07c2e-288">Edit the build definition (close it if it is already open), and select the **New** button if you do not yet see the new template in the list of Process Templates.</span></span>
10. <span data-ttu-id="07c2e-289">Set the parameter property values in the Misc section as follows:</span><span class="sxs-lookup"><span data-stu-id="07c2e-289">Set the parameter property values in the Misc section as follows:</span></span>

    1. <span data-ttu-id="07c2e-290">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span><span class="sxs-lookup"><span data-stu-id="07c2e-290">CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *This value is derived from: ($PublishDir)ServiceConfiguration.Cloud.cscfg*</span></span>
    2. <span data-ttu-id="07c2e-291">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span><span class="sxs-lookup"><span data-stu-id="07c2e-291">PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *This value is derived from: ($PublishDir)($ProjectName).cspkg*</span></span>
    3. <span data-ttu-id="07c2e-292">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span><span class="sxs-lookup"><span data-stu-id="07c2e-292">PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'</span></span>
    4. <span data-ttu-id="07c2e-293">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span><span class="sxs-lookup"><span data-stu-id="07c2e-293">ServiceName = 'mycloudservicename' *Use the appropriate cloud service name here*</span></span>
    5. <span data-ttu-id="07c2e-294">Environment = 'Staging'</span><span class="sxs-lookup"><span data-stu-id="07c2e-294">Environment = 'Staging'</span></span>
    6. <span data-ttu-id="07c2e-295">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span><span class="sxs-lookup"><span data-stu-id="07c2e-295">StorageAccountName = 'mystorageaccountname' *Use the appropriate storage account name here*</span></span>
    7. <span data-ttu-id="07c2e-296">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span><span class="sxs-lookup"><span data-stu-id="07c2e-296">SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'</span></span>
    8. <span data-ttu-id="07c2e-297">SubscriptionName = 'default'</span><span class="sxs-lookup"><span data-stu-id="07c2e-297">SubscriptionName = 'default'</span></span>

    ![Parameter property values][6]
11. <span data-ttu-id="07c2e-299">Save the changes to the Build Definition.</span><span class="sxs-lookup"><span data-stu-id="07c2e-299">Save the changes to the Build Definition.</span></span>
12. <span data-ttu-id="07c2e-300">Queue a Build to execute both the package build and publish.</span><span class="sxs-lookup"><span data-stu-id="07c2e-300">Queue a Build to execute both the package build and publish.</span></span> <span data-ttu-id="07c2e-301">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span><span class="sxs-lookup"><span data-stu-id="07c2e-301">If you have a trigger set to Continuous Integration, you will execute this behavior on every check-in.</span></span>

### <a name="publishcloudserviceps1-script-template"></a><span data-ttu-id="07c2e-302">PublishCloudService.ps1 script template</span><span class="sxs-lookup"><span data-stu-id="07c2e-302">PublishCloudService.ps1 script template</span></span>
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a><span data-ttu-id="07c2e-303">Next steps</span><span class="sxs-lookup"><span data-stu-id="07c2e-303">Next steps</span></span>
<span data-ttu-id="07c2e-304">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span><span class="sxs-lookup"><span data-stu-id="07c2e-304">To enable remote debugging when using continuous delivery, see [Enable remote debugging when using continuous delivery to publish to Azure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).</span></span>

[Continuous Delivery to Azure by Using Visual Studio Team Services]: cloud-services-continuous-delivery-use-vso.md
[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[the .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png






