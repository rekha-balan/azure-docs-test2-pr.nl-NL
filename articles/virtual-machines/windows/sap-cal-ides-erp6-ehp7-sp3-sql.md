---
title: Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure | Microsoft Docs
description: Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure
services: virtual-machines-windows
documentationcenter: ''
author: hermanndms
manager: timlt
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
ms.openlocfilehash: 9f5f22d9885bbd8426bbb315787d03b32072a951
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555570"
---
# <a name="deploying-sap-ides-ehp7-sp3-for-sap-erp-60-on-microsoft-azure"></a><span data-ttu-id="bcbae-103">Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bcbae-103">Deploying SAP IDES EHP7 SP3 for SAP ERP 6.0 on Microsoft Azure</span></span>
<span data-ttu-id="bcbae-104">This article describes how to deploy SAP IDES running with SQL Server and Windows OS on Microsoft Azure via SAP Cloud Appliance Library 3.0.</span><span class="sxs-lookup"><span data-stu-id="bcbae-104">This article describes how to deploy SAP IDES running with SQL Server and Windows OS on Microsoft Azure via SAP Cloud Appliance Library 3.0.</span></span> <span data-ttu-id="bcbae-105">The screenshots show the process step by step.</span><span class="sxs-lookup"><span data-stu-id="bcbae-105">The screenshots show the process step by step.</span></span> <span data-ttu-id="bcbae-106">Deploying other solutions in the list works the same way from a process perspective.</span><span class="sxs-lookup"><span data-stu-id="bcbae-106">Deploying other solutions in the list works the same way from a process perspective.</span></span> <span data-ttu-id="bcbae-107">One just has to select a different solution.</span><span class="sxs-lookup"><span data-stu-id="bcbae-107">One just has to select a different solution.</span></span>

<span data-ttu-id="bcbae-108">To start with SAP Cloud Appliance Library (SAP CAL) go [here](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="bcbae-108">To start with SAP Cloud Appliance Library (SAP CAL) go [here](https://cal.sap.com/).</span></span> <span data-ttu-id="bcbae-109">There is a blog from SAP about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="bcbae-109">There is a blog from SAP about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

<span data-ttu-id="bcbae-110">The following screenshots show step-by-step how to deploy SAP IDES on Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bcbae-110">The following screenshots show step-by-step how to deploy SAP IDES on Microsoft Azure.</span></span> <span data-ttu-id="bcbae-111">The process works the same way for other solutions.</span><span class="sxs-lookup"><span data-stu-id="bcbae-111">The process works the same way for other solutions.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

<span data-ttu-id="bcbae-112">The first picture shows all solutions that are available on Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bcbae-112">The first picture shows all solutions that are available on Microsoft Azure.</span></span> <span data-ttu-id="bcbae-113">The highlighted Windows-based SAP IDES solution that is only available on Azure was chosen to go through the process.</span><span class="sxs-lookup"><span data-stu-id="bcbae-113">The highlighted Windows-based SAP IDES solution that is only available on Azure was chosen to go through the process.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic2.jpg)

<span data-ttu-id="bcbae-114">First a new SAP CAL account has to be created.</span><span class="sxs-lookup"><span data-stu-id="bcbae-114">First a new SAP CAL account has to be created.</span></span> <span data-ttu-id="bcbae-115">There are currently two choices for Azure - standard Azure and Azure on China mainland that is operated by partner 21Vianet.</span><span class="sxs-lookup"><span data-stu-id="bcbae-115">There are currently two choices for Azure - standard Azure and Azure on China mainland that is operated by partner 21Vianet.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic3.jpg)

<span data-ttu-id="bcbae-116">Then one has to enter the Azure subscription ID that can be found on the Azure portal - also see further down how to get it.</span><span class="sxs-lookup"><span data-stu-id="bcbae-116">Then one has to enter the Azure subscription ID that can be found on the Azure portal - also see further down how to get it.</span></span> <span data-ttu-id="bcbae-117">Afterwards an Azure management certificate needs to be downloaded.</span><span class="sxs-lookup"><span data-stu-id="bcbae-117">Afterwards an Azure management certificate needs to be downloaded.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic6.jpg)

<span data-ttu-id="bcbae-118">In the new Azure portal one finds the item "Subscriptions" on the left side.</span><span class="sxs-lookup"><span data-stu-id="bcbae-118">In the new Azure portal one finds the item "Subscriptions" on the left side.</span></span> <span data-ttu-id="bcbae-119">Click it to show all active subscriptions for your user.</span><span class="sxs-lookup"><span data-stu-id="bcbae-119">Click it to show all active subscriptions for your user.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic7.jpg)

<span data-ttu-id="bcbae-120">Selecting one of the subscriptions and then choosing "Management Certificates" explains that there is a new concept using "service principals" for the new Azure Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="bcbae-120">Selecting one of the subscriptions and then choosing "Management Certificates" explains that there is a new concept using "service principals" for the new Azure Resource Manager model.</span></span>
<span data-ttu-id="bcbae-121">SAP CAL isn't adapted yet for this new model and still requires the "classic" model and the former Azure portal to work with management certificates.</span><span class="sxs-lookup"><span data-stu-id="bcbae-121">SAP CAL isn't adapted yet for this new model and still requires the "classic" model and the former Azure portal to work with management certificates.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic4.jpg)

<span data-ttu-id="bcbae-122">Here one can see the former Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bcbae-122">Here one can see the former Azure portal.</span></span> <span data-ttu-id="bcbae-123">The upload of a management certificate gives SAP CAL the permissions to create virtual machines within a customer subscription.</span><span class="sxs-lookup"><span data-stu-id="bcbae-123">The upload of a management certificate gives SAP CAL the permissions to create virtual machines within a customer subscription.</span></span> <span data-ttu-id="bcbae-124">Under the "SUBSCRIPTIONS" tab one can find the subscription ID that has to be entered in the SAP CAL portal.</span><span class="sxs-lookup"><span data-stu-id="bcbae-124">Under the "SUBSCRIPTIONS" tab one can find the subscription ID that has to be entered in the SAP CAL portal.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic5.jpg)

<span data-ttu-id="bcbae-125">On the second tab, it's then possible to upload the management certificate that was downloaded before from SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="bcbae-125">On the second tab, it's then possible to upload the management certificate that was downloaded before from SAP CAL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic8.jpg)

<span data-ttu-id="bcbae-126">A little dialog pops up to select the downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="bcbae-126">A little dialog pops up to select the downloaded certificate file.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic9.jpg)

<span data-ttu-id="bcbae-127">Once the certificate was uploaded the connection between SAP CAL and the customer Azure subscription can be tested within SAP CAl.</span><span class="sxs-lookup"><span data-stu-id="bcbae-127">Once the certificate was uploaded the connection between SAP CAL and the customer Azure subscription can be tested within SAP CAl.</span></span> <span data-ttu-id="bcbae-128">A little message should pop up which tells that the connection is valid.</span><span class="sxs-lookup"><span data-stu-id="bcbae-128">A little message should pop up which tells that the connection is valid.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic10.jpg)

<span data-ttu-id="bcbae-129">After the setup of an account one has to select a solution that should be deployed and create an instance.</span><span class="sxs-lookup"><span data-stu-id="bcbae-129">After the setup of an account one has to select a solution that should be deployed and create an instance.</span></span>
<span data-ttu-id="bcbae-130">With "basic" mode, it's really trivial.</span><span class="sxs-lookup"><span data-stu-id="bcbae-130">With "basic" mode, it's really trivial.</span></span> <span data-ttu-id="bcbae-131">Enter an instance name, choose an Azure region and define the master password for the solution.</span><span class="sxs-lookup"><span data-stu-id="bcbae-131">Enter an instance name, choose an Azure region and define the master password for the solution.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic11.jpg)

<span data-ttu-id="bcbae-132">After some time depending on the size and complexity of the solution (an estimation is given by SAP CAL) it's shown as "active" and ready for use.</span><span class="sxs-lookup"><span data-stu-id="bcbae-132">After some time depending on the size and complexity of the solution (an estimation is given by SAP CAL) it's shown as "active" and ready for use.</span></span> <span data-ttu-id="bcbae-133">It is very simple.</span><span class="sxs-lookup"><span data-stu-id="bcbae-133">It is very simple.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic12.jpg)

<span data-ttu-id="bcbae-134">Looking at some details of the solution one can see which kind of VMs were deployed.</span><span class="sxs-lookup"><span data-stu-id="bcbae-134">Looking at some details of the solution one can see which kind of VMs were deployed.</span></span> <span data-ttu-id="bcbae-135">In this case there is one single Azure VM of size D12 that was created by SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="bcbae-135">In this case there is one single Azure VM of size D12 that was created by SAP CAL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic13.jpg)

<span data-ttu-id="bcbae-136">On the Azure portal, the virtual machine can be found starting with the same instance name that was given in SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="bcbae-136">On the Azure portal, the virtual machine can be found starting with the same instance name that was given in SAP CAL.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic14.jpg)

<span data-ttu-id="bcbae-137">Now it's possible to connect to the solution via the connect button in the SAP CAL portal.</span><span class="sxs-lookup"><span data-stu-id="bcbae-137">Now it's possible to connect to the solution via the connect button in the SAP CAL portal.</span></span> <span data-ttu-id="bcbae-138">The little dialog contains a link to a user guide that describes all the default credentials to work with the solution.</span><span class="sxs-lookup"><span data-stu-id="bcbae-138">The little dialog contains a link to a user guide that describes all the default credentials to work with the solution.</span></span>
<span data-ttu-id="bcbae-139">[Here](https://caldocs.hana.ondemand.com/caldocs/help/Getting_Started_Guide_IDES607MSSQL.pdf) is the link to the guide for the IDES solution.</span><span class="sxs-lookup"><span data-stu-id="bcbae-139">[Here](https://caldocs.hana.ondemand.com/caldocs/help/Getting_Started_Guide_IDES607MSSQL.pdf) is the link to the guide for the IDES solution.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/sap-cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="bcbae-140">Another option is to login to the Windows VM and start for example the pre-configured SAP GUI.</span><span class="sxs-lookup"><span data-stu-id="bcbae-140">Another option is to login to the Windows VM and start for example the pre-configured SAP GUI.</span></span>
















