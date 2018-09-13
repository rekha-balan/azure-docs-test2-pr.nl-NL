---
title: Access on-premises data - Azure Logic Apps | Microsoft Docs
description: How your logic apps can access on-premises data by connecting to an on-premises data gateway.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/05/2016
ms.author: jehollan
ms.openlocfilehash: 8aa227e5c73233fbb9faab0e374f6365410adccb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550336"
---
# <a name="connect-to-on-premises-data-from-logic-apps"></a><span data-ttu-id="6cbec-103">Connect to on-premises data from logic apps</span><span class="sxs-lookup"><span data-stu-id="6cbec-103">Connect to on-premises data from logic apps</span></span>

<span data-ttu-id="6cbec-104">To access on-premises data, you can set up a connection to an on-premises data gateway for supported Azure Logic Apps connectors.</span><span class="sxs-lookup"><span data-stu-id="6cbec-104">To access on-premises data, you can set up a connection to an on-premises data gateway for supported Azure Logic Apps connectors.</span></span> <span data-ttu-id="6cbec-105">The following steps walk you through how to install and set up the on-premises data gateway to work with your logic apps.</span><span class="sxs-lookup"><span data-stu-id="6cbec-105">The following steps walk you through how to install and set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="6cbec-106">The on-premises data gateway supports these connections:</span><span class="sxs-lookup"><span data-stu-id="6cbec-106">The on-premises data gateway supports these connections:</span></span>

*   <span data-ttu-id="6cbec-107">BizTalk Server</span><span class="sxs-lookup"><span data-stu-id="6cbec-107">BizTalk Server</span></span>
*   <span data-ttu-id="6cbec-108">DB2</span><span class="sxs-lookup"><span data-stu-id="6cbec-108">DB2</span></span>  
*   <span data-ttu-id="6cbec-109">File System</span><span class="sxs-lookup"><span data-stu-id="6cbec-109">File System</span></span>
*   <span data-ttu-id="6cbec-110">Informix</span><span class="sxs-lookup"><span data-stu-id="6cbec-110">Informix</span></span>
*   <span data-ttu-id="6cbec-111">MQ</span><span class="sxs-lookup"><span data-stu-id="6cbec-111">MQ</span></span>
*   <span data-ttu-id="6cbec-112">MySQL</span><span class="sxs-lookup"><span data-stu-id="6cbec-112">MySQL</span></span>
*   <span data-ttu-id="6cbec-113">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="6cbec-113">Oracle Database</span></span> 
*   <span data-ttu-id="6cbec-114">SAP Application Server</span><span class="sxs-lookup"><span data-stu-id="6cbec-114">SAP Application Server</span></span> 
*   <span data-ttu-id="6cbec-115">SAP Message Server</span><span class="sxs-lookup"><span data-stu-id="6cbec-115">SAP Message Server</span></span>
*   <span data-ttu-id="6cbec-116">SharePoint for HTTP only, not HTTPS</span><span class="sxs-lookup"><span data-stu-id="6cbec-116">SharePoint for HTTP only, not HTTPS</span></span>
*   <span data-ttu-id="6cbec-117">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6cbec-117">SQL Server</span></span>
*   <span data-ttu-id="6cbec-118">Teradata</span><span class="sxs-lookup"><span data-stu-id="6cbec-118">Teradata</span></span>

<span data-ttu-id="6cbec-119">For more information about these connections, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="6cbec-119">For more information about these connections, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span>

## <a name="requirements"></a><span data-ttu-id="6cbec-120">Requirements</span><span class="sxs-lookup"><span data-stu-id="6cbec-120">Requirements</span></span>

* <span data-ttu-id="6cbec-121">You must have a work or school email address in Azure to associate the on-premises data gateway with your account (Azure Active Directory based account).</span><span class="sxs-lookup"><span data-stu-id="6cbec-121">You must have a work or school email address in Azure to associate the on-premises data gateway with your account (Azure Active Directory based account).</span></span>

* <span data-ttu-id="6cbec-122">If you are using a Microsoft account, like @outlook.com, you can use your Azure account to [create a work or school email address](../virtual-machines/windows/create-aad-work-id.md#locate-your-default-directory-in-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="6cbec-122">If you are using a Microsoft account, like @outlook.com, you can use your Azure account to [create a work or school email address](../virtual-machines/windows/create-aad-work-id.md#locate-your-default-directory-in-the-azure-classic-portal).</span></span>

* <span data-ttu-id="6cbec-123">You must have already [installed the on-premises data gateway on a local machine](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="6cbec-123">You must have already [installed the on-premises data gateway on a local machine](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="6cbec-124">You can associate your installation to one gateway resource only.</span><span class="sxs-lookup"><span data-stu-id="6cbec-124">You can associate your installation to one gateway resource only.</span></span> <span data-ttu-id="6cbec-125">Your gateway can't be claimed by another Azure on-premises data gateway.</span><span class="sxs-lookup"><span data-stu-id="6cbec-125">Your gateway can't be claimed by another Azure on-premises data gateway.</span></span> <span data-ttu-id="6cbec-126">Claim happens at ([creation during Step 2 in this topic](#2-create-an-azure-on-premises-data-gateway-resource)).</span><span class="sxs-lookup"><span data-stu-id="6cbec-126">Claim happens at ([creation during Step 2 in this topic](#2-create-an-azure-on-premises-data-gateway-resource)).</span></span>

## <a name="install-and-configure-the-connection"></a><span data-ttu-id="6cbec-127">Install and configure the connection</span><span class="sxs-lookup"><span data-stu-id="6cbec-127">Install and configure the connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="6cbec-128">1. Install the on-premises data gateway</span><span class="sxs-lookup"><span data-stu-id="6cbec-128">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="6cbec-129">If you haven't already, follow these steps to [install the on-premises data gateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="6cbec-129">If you haven't already, follow these steps to [install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="6cbec-130">Before you can continue with the other steps, make sure that you installed the data gateway on an on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="6cbec-130">Before you can continue with the other steps, make sure that you installed the data gateway on an on-premises machine.</span></span>

### <a name="2-create-an-azure-on-premises-data-gateway-resource"></a><span data-ttu-id="6cbec-131">2. Create an Azure on-premises data gateway resource</span><span class="sxs-lookup"><span data-stu-id="6cbec-131">2. Create an Azure on-premises data gateway resource</span></span>

<span data-ttu-id="6cbec-132">After you install the gateway, you must associate your Azure subscription with the gateway.</span><span class="sxs-lookup"><span data-stu-id="6cbec-132">After you install the gateway, you must associate your Azure subscription with the gateway.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6cbec-133">Ensure that the gateway resource is created in the same Azure region as your logic app.</span><span class="sxs-lookup"><span data-stu-id="6cbec-133">Ensure that the gateway resource is created in the same Azure region as your logic app.</span></span> <span data-ttu-id="6cbec-134">If you don't deploy the gateway resource to the same region, your logic app can't access the gateway.</span><span class="sxs-lookup"><span data-stu-id="6cbec-134">If you don't deploy the gateway resource to the same region, your logic app can't access the gateway.</span></span> 
> 

1. <span data-ttu-id="6cbec-135">Sign in to Azure using the same work or school email address that you used during gateway installation.</span><span class="sxs-lookup"><span data-stu-id="6cbec-135">Sign in to Azure using the same work or school email address that you used during gateway installation.</span></span>
2. <span data-ttu-id="6cbec-136">Choose **New**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-136">Choose **New**.</span></span>
3. <span data-ttu-id="6cbec-137">Find and select the **On-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-137">Find and select the **On-premises data gateway**.</span></span>
4. <span data-ttu-id="6cbec-138">To associate the gateway with your account, complete the information, including selecting the appropriate **Installation Name**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-138">To associate the gateway with your account, complete the information, including selecting the appropriate **Installation Name**.</span></span>
   
    ![On-Premises Data Gateway Connection][1]

5. <span data-ttu-id="6cbec-140">To create the resource, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-140">To create the resource, choose **Create**.</span></span>

### <a name="3-create-a-logic-app-connection-in-logic-app-designer"></a><span data-ttu-id="6cbec-141">3. Create a logic app connection in Logic App Designer</span><span class="sxs-lookup"><span data-stu-id="6cbec-141">3. Create a logic app connection in Logic App Designer</span></span>

<span data-ttu-id="6cbec-142">Now that your Azure subscription is associated with an instance of the on-premises data gateway, you can create a connection to the gateway from your logic app.</span><span class="sxs-lookup"><span data-stu-id="6cbec-142">Now that your Azure subscription is associated with an instance of the on-premises data gateway, you can create a connection to the gateway from your logic app.</span></span>

1. <span data-ttu-id="6cbec-143">Open a logic app and choose a connector that supports on-premises connectivity, like SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6cbec-143">Open a logic app and choose a connector that supports on-premises connectivity, like SQL Server.</span></span>
2. <span data-ttu-id="6cbec-144">Select **Connect via on-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-144">Select **Connect via on-premises data gateway**.</span></span>
   
    ![Logic App Designer Gateway Creation][2]

3. <span data-ttu-id="6cbec-146">Select the **Gateway** that you want to connect, and complete any other required connection information.</span><span class="sxs-lookup"><span data-stu-id="6cbec-146">Select the **Gateway** that you want to connect, and complete any other required connection information.</span></span>
4. <span data-ttu-id="6cbec-147">To create the connection, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-147">To create the connection, choose **Create**.</span></span>

<span data-ttu-id="6cbec-148">Your connection is now configured for your logic app to use.</span><span class="sxs-lookup"><span data-stu-id="6cbec-148">Your connection is now configured for your logic app to use.</span></span>

## <a name="edit-your-data-gateway-connection-settings"></a><span data-ttu-id="6cbec-149">Edit your data gateway connection settings</span><span class="sxs-lookup"><span data-stu-id="6cbec-149">Edit your data gateway connection settings</span></span>

<span data-ttu-id="6cbec-150">After you add the data gateway connection to your logic app, you might have to make changes so you can adjust settings specific to that connection.</span><span class="sxs-lookup"><span data-stu-id="6cbec-150">After you add the data gateway connection to your logic app, you might have to make changes so you can adjust settings specific to that connection.</span></span> <span data-ttu-id="6cbec-151">You can find the connection in either of two places:</span><span class="sxs-lookup"><span data-stu-id="6cbec-151">You can find the connection in either of two places:</span></span>

* <span data-ttu-id="6cbec-152">On the logic app blade, under **Development Tools**, select **API Connections**.</span><span class="sxs-lookup"><span data-stu-id="6cbec-152">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> <span data-ttu-id="6cbec-153">This list shows you all API Connections associated with your logic app, including your data gateway connection.</span><span class="sxs-lookup"><span data-stu-id="6cbec-153">This list shows you all API Connections associated with your logic app, including your data gateway connection.</span></span> <span data-ttu-id="6cbec-154">To view and modify that connection's settings, select that connection.</span><span class="sxs-lookup"><span data-stu-id="6cbec-154">To view and modify that connection's settings, select that connection.</span></span>

* <span data-ttu-id="6cbec-155">On the API Connections main blade, you can find all API Connections associated with your Azure subscription, including your data gateway connection.</span><span class="sxs-lookup"><span data-stu-id="6cbec-155">On the API Connections main blade, you can find all API Connections associated with your Azure subscription, including your data gateway connection.</span></span> <span data-ttu-id="6cbec-156">To view and modify the connection settings, select that connection.</span><span class="sxs-lookup"><span data-stu-id="6cbec-156">To view and modify the connection settings, select that connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cbec-157">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6cbec-157">Next Steps</span></span>

* [<span data-ttu-id="6cbec-158">Common examples and scenarios for logic apps</span><span class="sxs-lookup"><span data-stu-id="6cbec-158">Common examples and scenarios for logic apps</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="6cbec-159">Enterprise integration features</span><span class="sxs-lookup"><span data-stu-id="6cbec-159">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!-- Image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-gateway-connection/createblade.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-gateway-connection/blankconnection.png
[3]: ./media/logic-apps-logic-gateway-connection/checkbox.png


