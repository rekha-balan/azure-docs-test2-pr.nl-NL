---
title: Connect to an on-premises SAP system in Azure Logic Apps | Microsoft Docs
description: Connect to an on-premises SAP system from your logic app workflow through the on-premises data gateway
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: ''
ms.assetid: ''
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: padmavc; LADocs
ms.openlocfilehash: 01780622850072cad0085d199a7acd18a0a9314d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671758"
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="1a5ca-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span><span class="sxs-lookup"><span data-stu-id="1a5ca-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="1a5ca-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="1a5ca-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="1a5ca-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="1a5ca-107">Current limitations:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-107">Current limitations:</span></span> 
> - <span data-ttu-id="1a5ca-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="1a5ca-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="1a5ca-109">In this scenario, requests might get blocked.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="1a5ca-110">The file picker does not display all the available fields.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="1a5ca-111">In this scenario, you can manually add paths.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a5ca-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1a5ca-112">Prerequisites</span></span>

- <span data-ttu-id="1a5ca-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="1a5ca-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="1a5ca-115">The gateway must be installed on an on-premises machine before you can proceed.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="1a5ca-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="1a5ca-117">Use any of the following SAP versions:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="1a5ca-118">SAP Server</span><span class="sxs-lookup"><span data-stu-id="1a5ca-118">SAP Server</span></span>
        - <span data-ttu-id="1a5ca-119">SAP ECC 6.0 Unicode</span><span class="sxs-lookup"><span data-stu-id="1a5ca-119">SAP ECC 6.0 Unicode</span></span>
        - <span data-ttu-id="1a5ca-120">SAP ECC 6.0 Unicode with EHP 4.0</span><span class="sxs-lookup"><span data-stu-id="1a5ca-120">SAP ECC 6.0 Unicode with EHP 4.0</span></span>
        - <span data-ttu-id="1a5ca-121">SAP ECC 6.0 with EHP 7.0 and all EHP previous versions</span><span class="sxs-lookup"><span data-stu-id="1a5ca-121">SAP ECC 6.0 with EHP 7.0 and all EHP previous versions</span></span>
 
    - <span data-ttu-id="1a5ca-122">SAP Client</span><span class="sxs-lookup"><span data-stu-id="1a5ca-122">SAP Client</span></span>
        - <span data-ttu-id="1a5ca-123">SAP RFC SDK 7.20 UNICODE</span><span class="sxs-lookup"><span data-stu-id="1a5ca-123">SAP RFC SDK 7.20 UNICODE</span></span>
        - <span data-ttu-id="1a5ca-124">SAP .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="1a5ca-124">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="1a5ca-125">Add triggers and actions for connecting to your SAP system</span><span class="sxs-lookup"><span data-stu-id="1a5ca-125">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="1a5ca-126">The SAP connector has actions, but not triggers.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-126">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="1a5ca-127">So, we have to use another trigger at the start of the workflow.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-127">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="1a5ca-128">Add the Request/Response trigger, and then select **New step**.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-128">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="1a5ca-129">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-129">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![Select SAP Application Server or SAP Message Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="1a5ca-131">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-131">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="1a5ca-132">If you don't have an existing connection, you are prompted to create one.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-132">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="1a5ca-133">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-133">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Add connection string to SAP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="1a5ca-135">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-135">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Install a new gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="1a5ca-137">After you enter all the details, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-137">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="1a5ca-138">Logic Apps configures and tests the connection, making sure that the connection works properly.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-138">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="1a5ca-139">Enter a name for your SAP connection.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-139">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="1a5ca-140">The different SAP options are now available.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-140">The different SAP options are now available.</span></span> <span data-ttu-id="1a5ca-141">To find your IDOC category, select from the list.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-141">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="1a5ca-142">Or manually type in the path, and select the HTTP response in the **body** field:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-142">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![SAP action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="1a5ca-144">Add the action for creating an **HTTP Response**.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-144">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="1a5ca-145">The response message should be from the SAP output.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-145">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="1a5ca-146">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-146">Save your logic app.</span></span> <span data-ttu-id="1a5ca-147">Test it by sending an IDOC through the HTTP trigger URL.</span><span class="sxs-lookup"><span data-stu-id="1a5ca-147">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="1a5ca-148">After the IDOC is sent, wait for the response from the logic app:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-148">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="1a5ca-149">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1a5ca-149">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="1a5ca-150">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span><span class="sxs-lookup"><span data-stu-id="1a5ca-150">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="1a5ca-151">BAPI</span><span class="sxs-lookup"><span data-stu-id="1a5ca-151">BAPI</span></span>
- <span data-ttu-id="1a5ca-152">RFC</span><span class="sxs-lookup"><span data-stu-id="1a5ca-152">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="1a5ca-153">Get help</span><span class="sxs-lookup"><span data-stu-id="1a5ca-153">Get help</span></span>

<span data-ttu-id="1a5ca-154">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1a5ca-154">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1a5ca-155">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1a5ca-155">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a5ca-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a5ca-156">Next steps</span></span>

- <span data-ttu-id="1a5ca-157">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a5ca-157">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="1a5ca-158">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span><span class="sxs-lookup"><span data-stu-id="1a5ca-158">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>




