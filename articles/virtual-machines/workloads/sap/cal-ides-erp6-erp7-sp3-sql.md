---
title: Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure | Microsoft Docs
description: Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure
services: virtual-machines-windows
documentationcenter: ''
author: hermanndms
manager: jeconnoc
editor: ''
tags: azure-resource-manager
keywords: ''
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 93824c8f0e7667fcb58fd6b8292cddfa2b4a482a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830414"
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="7b47b-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span><span class="sxs-lookup"><span data-stu-id="7b47b-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="7b47b-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="7b47b-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="7b47b-105">The screenshots show the step-by-step process.</span><span class="sxs-lookup"><span data-stu-id="7b47b-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="7b47b-106">To deploy a different solution, follow the same steps.</span><span class="sxs-lookup"><span data-stu-id="7b47b-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="7b47b-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span><span class="sxs-lookup"><span data-stu-id="7b47b-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="7b47b-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="7b47b-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="7b47b-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7b47b-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="7b47b-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="7b47b-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="7b47b-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span><span class="sxs-lookup"><span data-stu-id="7b47b-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="7b47b-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="7b47b-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="7b47b-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span><span class="sxs-lookup"><span data-stu-id="7b47b-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="7b47b-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span><span class="sxs-lookup"><span data-stu-id="7b47b-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="7b47b-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span><span class="sxs-lookup"><span data-stu-id="7b47b-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![SAP CAL Solutions](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="7b47b-117">Create an account in the SAP CAL</span><span class="sxs-lookup"><span data-stu-id="7b47b-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="7b47b-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span><span class="sxs-lookup"><span data-stu-id="7b47b-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="7b47b-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span><span class="sxs-lookup"><span data-stu-id="7b47b-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="7b47b-120">In the account definition, you need to:</span><span class="sxs-lookup"><span data-stu-id="7b47b-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="7b47b-121">a.</span><span class="sxs-lookup"><span data-stu-id="7b47b-121">a.</span></span> <span data-ttu-id="7b47b-122">Select the deployment model on Azure (Resource Manager or classic).</span><span class="sxs-lookup"><span data-stu-id="7b47b-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="7b47b-123">b.</span><span class="sxs-lookup"><span data-stu-id="7b47b-123">b.</span></span> <span data-ttu-id="7b47b-124">Enter your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b47b-124">Enter your Azure subscription.</span></span> <span data-ttu-id="7b47b-125">An SAP CAL account can be assigned to one subscription only.</span><span class="sxs-lookup"><span data-stu-id="7b47b-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="7b47b-126">If you need more than one subscription, you need to create another SAP CAL account.</span><span class="sxs-lookup"><span data-stu-id="7b47b-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="7b47b-127">c.</span><span class="sxs-lookup"><span data-stu-id="7b47b-127">c.</span></span> <span data-ttu-id="7b47b-128">Give the SAP CAL permission to deploy into your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b47b-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="7b47b-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span><span class="sxs-lookup"><span data-stu-id="7b47b-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="7b47b-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span><span class="sxs-lookup"><span data-stu-id="7b47b-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="7b47b-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="7b47b-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

1. <span data-ttu-id="7b47b-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span><span class="sxs-lookup"><span data-stu-id="7b47b-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="7b47b-133">a.</span><span class="sxs-lookup"><span data-stu-id="7b47b-133">a.</span></span> <span data-ttu-id="7b47b-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span><span class="sxs-lookup"><span data-stu-id="7b47b-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="7b47b-135">b.</span><span class="sxs-lookup"><span data-stu-id="7b47b-135">b.</span></span> <span data-ttu-id="7b47b-136">**Microsoft Azure** is the new Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="7b47b-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![SAP CAL Accounts](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="7b47b-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL Accounts](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

1. <span data-ttu-id="7b47b-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b47b-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![SAP CAL Subscription ID](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

1. <span data-ttu-id="7b47b-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="7b47b-143">The following page appears in the browser tab:</span><span class="sxs-lookup"><span data-stu-id="7b47b-143">The following page appears in the browser tab:</span></span>

    ![Internet Explorer cloud services sign-in](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

1. <span data-ttu-id="7b47b-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span><span class="sxs-lookup"><span data-stu-id="7b47b-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="7b47b-146">The following page appears in the browser tab:</span><span class="sxs-lookup"><span data-stu-id="7b47b-146">The following page appears in the browser tab:</span></span>

    ![Internet Explorer cloud services confirmation](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

1. <span data-ttu-id="7b47b-148">Click **Accept**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-148">Click **Accept**.</span></span> <span data-ttu-id="7b47b-149">If the authorization is successful, the SAP CAL account definition displays again.</span><span class="sxs-lookup"><span data-stu-id="7b47b-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="7b47b-150">After a short time, a message confirms that the authorization process was successful.</span><span class="sxs-lookup"><span data-stu-id="7b47b-150">After a short time, a message confirms that the authorization process was successful.</span></span>

1. <span data-ttu-id="7b47b-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![Account to user association](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

1. <span data-ttu-id="7b47b-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

1. <span data-ttu-id="7b47b-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![User to account association](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="7b47b-156">You successfully created an SAP CAL account that is able to:</span><span class="sxs-lookup"><span data-stu-id="7b47b-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="7b47b-157">Use the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="7b47b-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="7b47b-158">Deploy SAP systems into your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7b47b-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="7b47b-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span><span class="sxs-lookup"><span data-stu-id="7b47b-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="7b47b-160">Otherwise, the solution might show up as **Locked** on the overview page.</span><span class="sxs-lookup"><span data-stu-id="7b47b-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="7b47b-161">Deploy a solution</span><span class="sxs-lookup"><span data-stu-id="7b47b-161">Deploy a solution</span></span>
1. <span data-ttu-id="7b47b-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span><span class="sxs-lookup"><span data-stu-id="7b47b-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="7b47b-163">Click **Create Instance**, and confirm the usage and terms conditions.</span><span class="sxs-lookup"><span data-stu-id="7b47b-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

1. <span data-ttu-id="7b47b-164">On the **Basic Mode: Create Instance** page, you need to:</span><span class="sxs-lookup"><span data-stu-id="7b47b-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="7b47b-165">a.</span><span class="sxs-lookup"><span data-stu-id="7b47b-165">a.</span></span> <span data-ttu-id="7b47b-166">Enter an instance **Name**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="7b47b-167">b.</span><span class="sxs-lookup"><span data-stu-id="7b47b-167">b.</span></span> <span data-ttu-id="7b47b-168">Select an Azure **Region**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-168">Select an Azure **Region**.</span></span> <span data-ttu-id="7b47b-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span><span class="sxs-lookup"><span data-stu-id="7b47b-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="7b47b-170">c.</span><span class="sxs-lookup"><span data-stu-id="7b47b-170">c.</span></span>  <span data-ttu-id="7b47b-171">Enter the master **Password** for the solution, as shown:</span><span class="sxs-lookup"><span data-stu-id="7b47b-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![SAP CAL Basic Mode: Create Instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

1. <span data-ttu-id="7b47b-173">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-173">Click **Create**.</span></span> <span data-ttu-id="7b47b-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span><span class="sxs-lookup"><span data-stu-id="7b47b-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![SAP CAL Instances](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

1. <span data-ttu-id="7b47b-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b47b-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="7b47b-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="7b47b-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![Resource group objects](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

1. <span data-ttu-id="7b47b-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="7b47b-180">The following pop-up window appears:</span><span class="sxs-lookup"><span data-stu-id="7b47b-180">The following pop-up window appears:</span></span> 

    ![Connect to the Instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

1. <span data-ttu-id="7b47b-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="7b47b-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="7b47b-183">The documentation names the users for each of the connectivity methods.</span><span class="sxs-lookup"><span data-stu-id="7b47b-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="7b47b-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span><span class="sxs-lookup"><span data-stu-id="7b47b-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="7b47b-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span><span class="sxs-lookup"><span data-stu-id="7b47b-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![SAP Welcome documentation](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="7b47b-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b47b-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="7b47b-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span><span class="sxs-lookup"><span data-stu-id="7b47b-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="7b47b-189">The support queue is BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="7b47b-189">The support queue is BC-VCM-CAL.</span></span>

