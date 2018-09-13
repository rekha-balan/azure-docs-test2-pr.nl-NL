---
title: Enable Remote Desktop Connection for a Role in Azure Cloud Services | Microsoft Docs
description: How to configure your azure cloud service application to allow remote desktop connections
services: cloud-services
documentationcenter: ''
author: seanmck
manager: timlt
editor: ''
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: seanmck
ms.openlocfilehash: a4b1eff8e762ed6d8b63d0e2ae66c66045f0f5e0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540883"
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="e9932-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e9932-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure classic portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="e9932-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span><span class="sxs-lookup"><span data-stu-id="e9932-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="e9932-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span><span class="sxs-lookup"><span data-stu-id="e9932-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="e9932-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span><span class="sxs-lookup"><span data-stu-id="e9932-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="e9932-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span><span class="sxs-lookup"><span data-stu-id="e9932-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="e9932-112">Configure Remote Desktop from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e9932-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="e9932-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="e9932-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="e9932-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span><span class="sxs-lookup"><span data-stu-id="e9932-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="e9932-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="e9932-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Cloud services remote desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="e9932-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="e9932-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="e9932-118">Fill in the required fields for user name, password, expiry, and certificate.</span><span class="sxs-lookup"><span data-stu-id="e9932-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Cloud services remote desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.PNG)

   > [!WARNING]
   > All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark). To prevent a reboot, the certificate used to encrypt the password must be installed on the role. To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.
   >
   >
3. <span data-ttu-id="e9932-123">In **Roles**, select the role you want to update or select **All** for all roles.</span><span class="sxs-lookup"><span data-stu-id="e9932-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="e9932-124">When you finish your configuration updates, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e9932-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="e9932-125">It will take a few moments before your role instances are ready to receive connections.</span><span class="sxs-lookup"><span data-stu-id="e9932-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="e9932-126">Remote into role instances</span><span class="sxs-lookup"><span data-stu-id="e9932-126">Remote into role instances</span></span>
<span data-ttu-id="e9932-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="e9932-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="e9932-128">Click **Instances** to open the **Instances** blade.</span><span class="sxs-lookup"><span data-stu-id="e9932-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="e9932-129">Select a role instance that has Remote Desktop configured.</span><span class="sxs-lookup"><span data-stu-id="e9932-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="e9932-130">Click **Connect** to download an RDP file for the role instance.</span><span class="sxs-lookup"><span data-stu-id="e9932-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Cloud services remote desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.PNG)

4. <span data-ttu-id="e9932-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span><span class="sxs-lookup"><span data-stu-id="e9932-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.  Remote Desktop uses port **3389**.  Cloud Service instances are load balanced, so you can't directly control which instance to connect to.  The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.  The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.

## <a name="additional-resources"></a><span data-ttu-id="e9932-138">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e9932-138">Additional resources</span></span>

<span data-ttu-id="e9932-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md#remote-desktop)</span><span class="sxs-lookup"><span data-stu-id="e9932-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md#remote-desktop)</span></span>



