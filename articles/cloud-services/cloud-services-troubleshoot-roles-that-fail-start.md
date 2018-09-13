---
title: Troubleshoot roles that fail to start | Microsoft Docs
description: Here are some common reasons why a Cloud Service role may fail to start. Solutions to these problems are also provided.
services: cloud-services
documentationcenter: ''
author: simonxjx
manager: felixwu
editor: ''
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/15/2018
ms.author: v-six
ms.openlocfilehash: 4b4669ecdae474c8926a346ed02f40913cf67265
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775573"
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="f08d2-104">Troubleshoot Cloud Service roles that fail to start</span><span class="sxs-lookup"><span data-stu-id="f08d2-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="f08d2-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span><span class="sxs-lookup"><span data-stu-id="f08d2-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="f08d2-106">Missing DLLs or dependencies</span><span class="sxs-lookup"><span data-stu-id="f08d2-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="f08d2-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span><span class="sxs-lookup"><span data-stu-id="f08d2-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="f08d2-108">Symptoms of missing DLLs or assemblies can be:</span><span class="sxs-lookup"><span data-stu-id="f08d2-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="f08d2-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span><span class="sxs-lookup"><span data-stu-id="f08d2-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="f08d2-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span><span class="sxs-lookup"><span data-stu-id="f08d2-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="f08d2-111">There are several recommended methods for investigating these issues.</span><span class="sxs-lookup"><span data-stu-id="f08d2-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="f08d2-112">Diagnose missing DLL issues in a web role</span><span class="sxs-lookup"><span data-stu-id="f08d2-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="f08d2-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span><span class="sxs-lookup"><span data-stu-id="f08d2-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

![Server Error in '/' Application.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="f08d2-115">Diagnose issues by turning off custom errors</span><span class="sxs-lookup"><span data-stu-id="f08d2-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="f08d2-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span><span class="sxs-lookup"><span data-stu-id="f08d2-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="f08d2-117">To view more complete errors without using Remote Desktop:</span><span class="sxs-lookup"><span data-stu-id="f08d2-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="f08d2-118">Open the solution in Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f08d2-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="f08d2-119">In the **Solution Explorer**, locate the web.config file and open it.</span><span class="sxs-lookup"><span data-stu-id="f08d2-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="f08d2-120">In the web.config file, locate the system.web section and add the following line:</span><span class="sxs-lookup"><span data-stu-id="f08d2-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="f08d2-121">Save the file.</span><span class="sxs-lookup"><span data-stu-id="f08d2-121">Save the file.</span></span>
5. <span data-ttu-id="f08d2-122">Repackage and redeploy the service.</span><span class="sxs-lookup"><span data-stu-id="f08d2-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="f08d2-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span><span class="sxs-lookup"><span data-stu-id="f08d2-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="f08d2-124">Diagnose issues by viewing the error remotely</span><span class="sxs-lookup"><span data-stu-id="f08d2-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="f08d2-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span><span class="sxs-lookup"><span data-stu-id="f08d2-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="f08d2-126">Use the following steps to view the errors by using Remote Desktop:</span><span class="sxs-lookup"><span data-stu-id="f08d2-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="f08d2-127">Ensure that Azure SDK 1.3 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="f08d2-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="f08d2-128">During the deployment of the solution by using Visual Studio, enable Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="f08d2-128">During the deployment of the solution by using Visual Studio, enable Remote Desktop.</span></span> <span data-ttu-id="f08d2-129">For more information, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services using Visual Studio](cloud-services-role-enable-remote-desktop-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f08d2-129">For more information, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services using Visual Studio](cloud-services-role-enable-remote-desktop-visual-studio.md).</span></span>
3. <span data-ttu-id="f08d2-130">In the Microsoft Azure portal, once the instance shows a status of **Ready**, remote into the instance.</span><span class="sxs-lookup"><span data-stu-id="f08d2-130">In the Microsoft Azure portal, once the instance shows a status of **Ready**, remote into the instance.</span></span> <span data-ttu-id="f08d2-131">For more information on using the remote desktop with Cloud Services, see [Remote into role instances](cloud-services-role-enable-remote-desktop-new-portal.md#remote-into-role-instances).</span><span class="sxs-lookup"><span data-stu-id="f08d2-131">For more information on using the remote desktop with Cloud Services, see [Remote into role instances](cloud-services-role-enable-remote-desktop-new-portal.md#remote-into-role-instances).</span></span>
5. <span data-ttu-id="f08d2-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span><span class="sxs-lookup"><span data-stu-id="f08d2-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="f08d2-133">Open a command window.</span><span class="sxs-lookup"><span data-stu-id="f08d2-133">Open a command window.</span></span>
7. <span data-ttu-id="f08d2-134">Type `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="f08d2-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="f08d2-135">Note the IPV4 Address value.</span><span class="sxs-lookup"><span data-stu-id="f08d2-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="f08d2-136">Open Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f08d2-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="f08d2-137">Type the address and the name of the web application.</span><span class="sxs-lookup"><span data-stu-id="f08d2-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="f08d2-138">For example, `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="f08d2-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="f08d2-139">Navigating to the website will now return more explicit error messages:</span><span class="sxs-lookup"><span data-stu-id="f08d2-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="f08d2-140">Server Error in '/' Application.</span><span class="sxs-lookup"><span data-stu-id="f08d2-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="f08d2-141">Description: An unhandled exception occurred during the execution of the current web request.</span><span class="sxs-lookup"><span data-stu-id="f08d2-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="f08d2-142">Please review the stack trace for more information about the error and where it originated in the code.</span><span class="sxs-lookup"><span data-stu-id="f08d2-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="f08d2-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span><span class="sxs-lookup"><span data-stu-id="f08d2-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="f08d2-144">The system cannot find the file specified.</span><span class="sxs-lookup"><span data-stu-id="f08d2-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="f08d2-145">For example:</span><span class="sxs-lookup"><span data-stu-id="f08d2-145">For example:</span></span>

![Explicit Server Error in '/' Application](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="f08d2-147">Diagnose issues by using the compute emulator</span><span class="sxs-lookup"><span data-stu-id="f08d2-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="f08d2-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span><span class="sxs-lookup"><span data-stu-id="f08d2-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="f08d2-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span><span class="sxs-lookup"><span data-stu-id="f08d2-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="f08d2-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="f08d2-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="f08d2-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f08d2-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f08d2-152">On the development machine, build the cloud service project.</span><span class="sxs-lookup"><span data-stu-id="f08d2-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="f08d2-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span><span class="sxs-lookup"><span data-stu-id="f08d2-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="f08d2-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span><span class="sxs-lookup"><span data-stu-id="f08d2-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="f08d2-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="f08d2-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="f08d2-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="f08d2-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="f08d2-157">When the role starts, you will see detailed error information in Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f08d2-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="f08d2-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span><span class="sxs-lookup"><span data-stu-id="f08d2-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="f08d2-159">Diagnose issues by using IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="f08d2-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="f08d2-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f08d2-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="f08d2-161">Follow these steps to deploy the service with IntelliTrace enabled:</span><span class="sxs-lookup"><span data-stu-id="f08d2-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="f08d2-162">Confirm that Azure SDK 1.3 or later is installed.</span><span class="sxs-lookup"><span data-stu-id="f08d2-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="f08d2-163">Deploy the solution by using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f08d2-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="f08d2-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span><span class="sxs-lookup"><span data-stu-id="f08d2-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="f08d2-165">Once the instance starts, open the **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f08d2-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="f08d2-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span><span class="sxs-lookup"><span data-stu-id="f08d2-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="f08d2-167">Expand the deployment until you see the role instances.</span><span class="sxs-lookup"><span data-stu-id="f08d2-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="f08d2-168">Right-click on one of the instances.</span><span class="sxs-lookup"><span data-stu-id="f08d2-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="f08d2-169">Choose **View IntelliTrace logs**.</span><span class="sxs-lookup"><span data-stu-id="f08d2-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="f08d2-170">The **IntelliTrace Summary** will open.</span><span class="sxs-lookup"><span data-stu-id="f08d2-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="f08d2-171">Locate the exceptions section of the summary.</span><span class="sxs-lookup"><span data-stu-id="f08d2-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="f08d2-172">If there are exceptions, the section will be labeled **Exception Data**.</span><span class="sxs-lookup"><span data-stu-id="f08d2-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="f08d2-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f08d2-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Exception data, missing file, or assembly](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="f08d2-175">Address missing DLLs and assemblies</span><span class="sxs-lookup"><span data-stu-id="f08d2-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="f08d2-176">To address missing DLL and assembly errors, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f08d2-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="f08d2-177">Open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f08d2-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="f08d2-178">In **Solution Explorer**, open the **References** folder.</span><span class="sxs-lookup"><span data-stu-id="f08d2-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="f08d2-179">Click the assembly identified in the error.</span><span class="sxs-lookup"><span data-stu-id="f08d2-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="f08d2-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span><span class="sxs-lookup"><span data-stu-id="f08d2-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="f08d2-181">Redeploy the cloud service.</span><span class="sxs-lookup"><span data-stu-id="f08d2-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="f08d2-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span><span class="sxs-lookup"><span data-stu-id="f08d2-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f08d2-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="f08d2-183">Next steps</span></span>
<span data-ttu-id="f08d2-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span><span class="sxs-lookup"><span data-stu-id="f08d2-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="f08d2-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="f08d2-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
