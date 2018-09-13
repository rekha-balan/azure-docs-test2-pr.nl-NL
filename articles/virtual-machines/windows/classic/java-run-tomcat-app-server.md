---
title: Run Java application server on a classic Azure VM | Microsoft Docs
description: This tutorial uses resources created with  the classic deployment model, and shows how to create a Windows Virtual machine and configure it to run Apache Tomcat application server.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 0387ff0c97cb634a9fc4ea67ee8a81a19d85df6b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551461"
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="8f952-103">How to run a Java application server on a virtual machine created with the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="8f952-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8f952-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8f952-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8f952-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="8f952-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8f952-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="8f952-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8f952-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="8f952-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="8f952-108">With Azure, you can use a virtual machine to provide server capabilities.</span><span class="sxs-lookup"><span data-stu-id="8f952-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="8f952-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="8f952-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="8f952-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span><span class="sxs-lookup"><span data-stu-id="8f952-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="8f952-111">You will learn and perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8f952-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="8f952-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span><span class="sxs-lookup"><span data-stu-id="8f952-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="8f952-113">How to remotely sign in to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="8f952-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="8f952-115">How to create an endpoint for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="8f952-116">How to open a port in the firewall for your application server.</span><span class="sxs-lookup"><span data-stu-id="8f952-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="8f952-117">The completed installation results in Tomcat running on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Virtual machine running Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="8f952-119">To create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="8f952-119">To create a virtual machine</span></span>
1. <span data-ttu-id="8f952-120">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f952-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="8f952-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span><span class="sxs-lookup"><span data-stu-id="8f952-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="8f952-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span><span class="sxs-lookup"><span data-stu-id="8f952-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="8f952-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span><span class="sxs-lookup"><span data-stu-id="8f952-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="8f952-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8f952-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="8f952-125">In the **Basics** blade:</span><span class="sxs-lookup"><span data-stu-id="8f952-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="8f952-126">Specify a name for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="8f952-127">Enter a name for the administrator in the **User Name** field.</span><span class="sxs-lookup"><span data-stu-id="8f952-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="8f952-128">Remember this name and the associated password that follows in the next field.</span><span class="sxs-lookup"><span data-stu-id="8f952-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="8f952-129">You need them when you remotely sign in to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="8f952-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span><span class="sxs-lookup"><span data-stu-id="8f952-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="8f952-131">This password is for the Administrator account.</span><span class="sxs-lookup"><span data-stu-id="8f952-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="8f952-132">Select the appropriate **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="8f952-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="8f952-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span><span class="sxs-lookup"><span data-stu-id="8f952-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="8f952-134">Or, click **Use existing** and select one of the available resource groups.</span><span class="sxs-lookup"><span data-stu-id="8f952-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="8f952-135">Select a location where the virtual machine resides, such as **South Central US**.</span><span class="sxs-lookup"><span data-stu-id="8f952-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="8f952-136">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f952-136">Click **Next**.</span></span>
7. <span data-ttu-id="8f952-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span><span class="sxs-lookup"><span data-stu-id="8f952-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="8f952-138">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="8f952-138">Click **Select**.</span></span>

9. <span data-ttu-id="8f952-139">In the **Settings** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f952-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="8f952-140">You can use the default values provided by Azure.</span><span class="sxs-lookup"><span data-stu-id="8f952-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="8f952-141">In the **Summary** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f952-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="8f952-142">To remotely sign in to your virtual machine</span><span class="sxs-lookup"><span data-stu-id="8f952-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="8f952-143">Log on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f952-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f952-144">Click **Virtual machines (classic)**.</span><span class="sxs-lookup"><span data-stu-id="8f952-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="8f952-145">If needed, click **More services** at the bottom left corner under the service categories.</span><span class="sxs-lookup"><span data-stu-id="8f952-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="8f952-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span><span class="sxs-lookup"><span data-stu-id="8f952-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="8f952-147">Click the name of the virtual machine that you want to sign in to.</span><span class="sxs-lookup"><span data-stu-id="8f952-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="8f952-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span><span class="sxs-lookup"><span data-stu-id="8f952-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="8f952-149">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="8f952-149">Click **Connect**.</span></span>
6. <span data-ttu-id="8f952-150">Respond to the prompts as needed to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="8f952-151">Typically, you save or open the .rdp file that contains the connection details.</span><span class="sxs-lookup"><span data-stu-id="8f952-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="8f952-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span><span class="sxs-lookup"><span data-stu-id="8f952-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="8f952-153">To install a Java application server on your virtual machine</span><span class="sxs-lookup"><span data-stu-id="8f952-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="8f952-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span><span class="sxs-lookup"><span data-stu-id="8f952-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="8f952-155">This tutorial uses Tomcat as the Java application server to install.</span><span class="sxs-lookup"><span data-stu-id="8f952-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="8f952-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="8f952-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="8f952-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span><span class="sxs-lookup"><span data-stu-id="8f952-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="8f952-158">By using this technique, Tomcat installs as a Windows service.</span><span class="sxs-lookup"><span data-stu-id="8f952-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="8f952-159">When prompted, choose to run the installer.</span><span class="sxs-lookup"><span data-stu-id="8f952-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="8f952-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span><span class="sxs-lookup"><span data-stu-id="8f952-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="8f952-161">For the purposes of this tutorial, accepting the defaults is fine.</span><span class="sxs-lookup"><span data-stu-id="8f952-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="8f952-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span><span class="sxs-lookup"><span data-stu-id="8f952-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="8f952-163">Click **Finish** to complete the Tomcat setup process.</span><span class="sxs-lookup"><span data-stu-id="8f952-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="8f952-164">To start Tomcat</span><span class="sxs-lookup"><span data-stu-id="8f952-164">To start Tomcat</span></span>

<span data-ttu-id="8f952-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="8f952-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="8f952-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span><span class="sxs-lookup"><span data-stu-id="8f952-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="8f952-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span><span class="sxs-lookup"><span data-stu-id="8f952-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="8f952-168">To create an endpoint for your virtual machine</span><span class="sxs-lookup"><span data-stu-id="8f952-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="8f952-169">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f952-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f952-170">Click **Virtual machines (classic)**.</span><span class="sxs-lookup"><span data-stu-id="8f952-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="8f952-171">Click the name of the virtual machine that is running your Java application server.</span><span class="sxs-lookup"><span data-stu-id="8f952-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="8f952-172">Click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="8f952-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="8f952-173">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8f952-173">Click **Add**.</span></span>
6. <span data-ttu-id="8f952-174">In the **Add endpoint** dialog box:</span><span class="sxs-lookup"><span data-stu-id="8f952-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="8f952-175">Specify a name for the endpoint; for example, **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="8f952-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="8f952-176">Select **TCP** for the protocol.</span><span class="sxs-lookup"><span data-stu-id="8f952-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="8f952-177">Specify **80** for the public port.</span><span class="sxs-lookup"><span data-stu-id="8f952-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="8f952-178">Specify **8080** for the private port.</span><span class="sxs-lookup"><span data-stu-id="8f952-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="8f952-179">Select **Disabled** for the floating IP address.</span><span class="sxs-lookup"><span data-stu-id="8f952-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="8f952-180">Leave the access control list as is.</span><span class="sxs-lookup"><span data-stu-id="8f952-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="8f952-181">Click the **OK** button to close the dialog box and create the endpoint.</span><span class="sxs-lookup"><span data-stu-id="8f952-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="8f952-182">To open a port in the firewall for your virtual machine</span><span class="sxs-lookup"><span data-stu-id="8f952-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="8f952-183">Sign in to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="8f952-184">Click **Windows Start**.</span><span class="sxs-lookup"><span data-stu-id="8f952-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="8f952-185">Click **Control Panel**.</span><span class="sxs-lookup"><span data-stu-id="8f952-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="8f952-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span><span class="sxs-lookup"><span data-stu-id="8f952-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="8f952-187">Click **Inbound Rules**, and then click **New Rule**.</span><span class="sxs-lookup"><span data-stu-id="8f952-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="8f952-188">![New inbound rule][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="8f952-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="8f952-189">For the **Rule Type**, select **Port**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f952-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="8f952-190">![New inbound rule port][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="8f952-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="8f952-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f952-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="8f952-192">![New inbound rule ][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="8f952-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="8f952-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f952-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="8f952-194">![New inbound rule action][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="8f952-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="8f952-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f952-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="8f952-196">![New inbound rule profile][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="8f952-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="8f952-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8f952-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="8f952-198">![New inbound rule name][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="8f952-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="8f952-199">At this point, your Tomcat website should be viewable from an external browser.</span><span class="sxs-lookup"><span data-stu-id="8f952-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="8f952-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8f952-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="8f952-201">Application lifecycle considerations</span><span class="sxs-lookup"><span data-stu-id="8f952-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="8f952-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span><span class="sxs-lookup"><span data-stu-id="8f952-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="8f952-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span><span class="sxs-lookup"><span data-stu-id="8f952-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="8f952-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span><span class="sxs-lookup"><span data-stu-id="8f952-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="8f952-205">By default when the Tomcat service is installed, it is set to start manually.</span><span class="sxs-lookup"><span data-stu-id="8f952-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="8f952-206">You can switch it to start automatically by using the Services snap-in.</span><span class="sxs-lookup"><span data-stu-id="8f952-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="8f952-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span><span class="sxs-lookup"><span data-stu-id="8f952-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="8f952-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span><span class="sxs-lookup"><span data-stu-id="8f952-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![Setting a service to start automatically][service_automatic_startup]

    <span data-ttu-id="8f952-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span><span class="sxs-lookup"><span data-stu-id="8f952-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f952-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f952-211">Next steps</span></span>
<span data-ttu-id="8f952-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span><span class="sxs-lookup"><span data-stu-id="8f952-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="8f952-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="8f952-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->








