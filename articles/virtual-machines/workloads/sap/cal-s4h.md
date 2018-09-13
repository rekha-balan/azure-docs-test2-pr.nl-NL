---
title: Deploy SAP S/4HANA or BW/4HANA on an Azure VM | Microsoft Docs
description: Deploy SAP S/4HANA or BW/4HANA on an Azure VM
services: virtual-machines-linux
documentationcenter: ''
author: hermanndms
manager: timlt
editor: ''
tags: azure-resource-manager
keywords: ''
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 659638b4db5961d736905c9f9ab55b7ed1129b65
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551261"
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-microsoft-azure"></a><span data-ttu-id="b04ba-103">Deploy SAP S/4HANA or BW/4HANA on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b04ba-103">Deploy SAP S/4HANA or BW/4HANA on Microsoft Azure</span></span>
<span data-ttu-id="b04ba-104">This article describes how to deploy S/4HANA on Microsoft Azure by using SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="b04ba-104">This article describes how to deploy S/4HANA on Microsoft Azure by using SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="b04ba-105">Deploying other SAP HANA-based solutions, like BW/4HANA, works the same way from a process perspective.</span><span class="sxs-lookup"><span data-stu-id="b04ba-105">Deploying other SAP HANA-based solutions, like BW/4HANA, works the same way from a process perspective.</span></span> <span data-ttu-id="b04ba-106">You just select a different solution.</span><span class="sxs-lookup"><span data-stu-id="b04ba-106">You just select a different solution.</span></span>

> [!NOTE]
<span data-ttu-id="b04ba-107">For more information about the SAP Cloud Appliance Library, see the [home page of their site](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="b04ba-107">For more information about the SAP Cloud Appliance Library, see the [home page of their site](https://cal.sap.com/).</span></span> <span data-ttu-id="b04ba-108">There is also a blog from SAP about [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="b04ba-108">There is also a blog from SAP about [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="b04ba-109">Step-by-step process to deploy the solution</span><span class="sxs-lookup"><span data-stu-id="b04ba-109">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="b04ba-110">The following screenshots show how to deploy S/4HANA on Azure.</span><span class="sxs-lookup"><span data-stu-id="b04ba-110">The following screenshots show how to deploy S/4HANA on Azure.</span></span> <span data-ttu-id="b04ba-111">The process works the same way for other solutions, like BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="b04ba-111">The process works the same way for other solutions, like BW/4HANA.</span></span>

<span data-ttu-id="b04ba-112">The first screenshot shows all SAP CAL HANA-based solutions available on Azure.</span><span class="sxs-lookup"><span data-stu-id="b04ba-112">The first screenshot shows all SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="b04ba-113">Notice **SAP S/4HANA on-premises edition** at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b04ba-113">Notice **SAP S/4HANA on-premises edition** at the bottom.</span></span>

![Screenshot of the SAP Cloud Appliance Library Solutions window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic-1b.jpg)

<span data-ttu-id="b04ba-115">First, create a new SAP CAL account.</span><span class="sxs-lookup"><span data-stu-id="b04ba-115">First, create a new SAP CAL account.</span></span> <span data-ttu-id="b04ba-116">In **Accounts**, you see two choices for Azure: Microsoft Azure, and an Azure option operated by 21Vianet.</span><span class="sxs-lookup"><span data-stu-id="b04ba-116">In **Accounts**, you see two choices for Azure: Microsoft Azure, and an Azure option operated by 21Vianet.</span></span> <span data-ttu-id="b04ba-117">For this example, choose **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b04ba-117">For this example, choose **Microsoft Azure**.</span></span>

![Screenshot of the SAP Cloud Appliance Library Accounts window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic-2.jpg)

<span data-ttu-id="b04ba-119">Then, enter the Azure subscription ID that can be found on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b04ba-119">Then, enter the Azure subscription ID that can be found on the Azure portal.</span></span> <span data-ttu-id="b04ba-120">Afterward, download an Azure management certificate.</span><span class="sxs-lookup"><span data-stu-id="b04ba-120">Afterward, download an Azure management certificate.</span></span>

![Screenshot of the SAP Cloud Appliance Library Accounts window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic3b.jpg)

> [!NOTE]
<span data-ttu-id="b04ba-122">To find your Azure subscription ID, you should use the Azure classic portal, not the more recent Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b04ba-122">To find your Azure subscription ID, you should use the Azure classic portal, not the more recent Azure portal.</span></span> <span data-ttu-id="b04ba-123">This is because SAP CAL isn't adapted yet for the new model, and still requires the classic portal to work with management certificates.</span><span class="sxs-lookup"><span data-stu-id="b04ba-123">This is because SAP CAL isn't adapted yet for the new model, and still requires the classic portal to work with management certificates.</span></span>

<span data-ttu-id="b04ba-124">The following screenshot shows the classic portal.</span><span class="sxs-lookup"><span data-stu-id="b04ba-124">The following screenshot shows the classic portal.</span></span> <span data-ttu-id="b04ba-125">From **SETTINGS**, select the **SUBSCRIPTIONS** tab to find the subscription ID to be entered in the SAP CAL Accounts window.</span><span class="sxs-lookup"><span data-stu-id="b04ba-125">From **SETTINGS**, select the **SUBSCRIPTIONS** tab to find the subscription ID to be entered in the SAP CAL Accounts window.</span></span>

![Screenshot of the Azure classic portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic4b.jpg)

<span data-ttu-id="b04ba-127">From **SETTINGS**, switch to the **MANAGEMENT CERTIFICATES** tab. Upload a management certificate to give SAP CAL the permissions to create virtual machines within a customer subscription.</span><span class="sxs-lookup"><span data-stu-id="b04ba-127">From **SETTINGS**, switch to the **MANAGEMENT CERTIFICATES** tab. Upload a management certificate to give SAP CAL the permissions to create virtual machines within a customer subscription.</span></span> <span data-ttu-id="b04ba-128">(You are uploading the management certificate that was downloaded before from SAP CAL.)</span><span class="sxs-lookup"><span data-stu-id="b04ba-128">(You are uploading the management certificate that was downloaded before from SAP CAL.)</span></span>

![Screenshot of the Azure classic portal, Management Certificates tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic5.jpg)

<span data-ttu-id="b04ba-130">A dialog box pops up for you to select the downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="b04ba-130">A dialog box pops up for you to select the downloaded certificate file.</span></span>

![Screenshot of Upload a management certificate dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic8.jpg)

<span data-ttu-id="b04ba-132">After the certificate is uploaded, the connection between SAP CAL and the Azure subscription can be tested within SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="b04ba-132">After the certificate is uploaded, the connection between SAP CAL and the Azure subscription can be tested within SAP CAL.</span></span> <span data-ttu-id="b04ba-133">A message should pop up that indicates that the connection is valid.</span><span class="sxs-lookup"><span data-stu-id="b04ba-133">A message should pop up that indicates that the connection is valid.</span></span>

![Screenshot of SAP Cloud Appliance Library Accounts window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic9.jpg)

<span data-ttu-id="b04ba-135">Next, select a solution that should be deployed, and create an instance.</span><span class="sxs-lookup"><span data-stu-id="b04ba-135">Next, select a solution that should be deployed, and create an instance.</span></span>
<span data-ttu-id="b04ba-136">Enter an instance name, choose an Azure region, and define the master password for the solution.</span><span class="sxs-lookup"><span data-stu-id="b04ba-136">Enter an instance name, choose an Azure region, and define the master password for the solution.</span></span>

![Screenshot of SAP Cloud Appliance Library Solutions window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic10.jpg)

<span data-ttu-id="b04ba-138">After some time, depending on the size and complexity of the solution (an estimate is provided by SAP CAL), the solution is shown as active and ready for use.</span><span class="sxs-lookup"><span data-stu-id="b04ba-138">After some time, depending on the size and complexity of the solution (an estimate is provided by SAP CAL), the solution is shown as active and ready for use.</span></span>

![Screenshot of SAP Cloud Appliance Library Instances window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic11.jpg)

<span data-ttu-id="b04ba-140">You can see some details of the solution, such as which kind of VMs were deployed.</span><span class="sxs-lookup"><span data-stu-id="b04ba-140">You can see some details of the solution, such as which kind of VMs were deployed.</span></span> <span data-ttu-id="b04ba-141">In this case, three Azure VMs of different sizes and purpose were created.</span><span class="sxs-lookup"><span data-stu-id="b04ba-141">In this case, three Azure VMs of different sizes and purpose were created.</span></span>

![Screenshot of SAP Cloud Appliance Library Instances window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic12.jpg)

<span data-ttu-id="b04ba-143">In the Azure classic portal, these virtual machines can be found starting with the same instance name that was given in SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="b04ba-143">In the Azure classic portal, these virtual machines can be found starting with the same instance name that was given in SAP CAL.</span></span>

![Screenshot that shows three virtual machines in the Azure classic portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic13.jpg)

<span data-ttu-id="b04ba-145">Now it's possible to connect to the solution by using the connect button in the SAP CAL portal.</span><span class="sxs-lookup"><span data-stu-id="b04ba-145">Now it's possible to connect to the solution by using the connect button in the SAP CAL portal.</span></span> <span data-ttu-id="b04ba-146">The dialog box contains a link to a user guide that describes all the default credentials to work with the solution.</span><span class="sxs-lookup"><span data-stu-id="b04ba-146">The dialog box contains a link to a user guide that describes all the default credentials to work with the solution.</span></span>

![Screenshot of Connect to the Instance dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic14b.jpg)

<span data-ttu-id="b04ba-148">Another option is to sign in to the client Windows VM, and start the pre-configured SAP GUI, for example.</span><span class="sxs-lookup"><span data-stu-id="b04ba-148">Another option is to sign in to the client Windows VM, and start the pre-configured SAP GUI, for example.</span></span>

![Screenshot of the pre-configured SAP GUI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/workloads/sap/media/cal-s4h/s4h-pic15.jpg)













