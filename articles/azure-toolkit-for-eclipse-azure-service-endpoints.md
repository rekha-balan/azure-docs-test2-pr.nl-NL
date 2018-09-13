---
title: Azure Service Endpoints
description: Describes the Azure Service Endpoint settings in the Azure Toolkit for Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 820e960b130b047b407950474dc036802f559298
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553767"
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="0f2b5-103">Azure Service Endpoints</span><span class="sxs-lookup"><span data-stu-id="0f2b5-103">Azure Service Endpoints</span></span>
<span data-ttu-id="0f2b5-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="0f2b5-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="0f2b5-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="0f2b5-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="0f2b5-108">The following shows the **Service Endpoints** dialog.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="0f2b5-109">To set the service endpoints</span><span class="sxs-lookup"><span data-stu-id="0f2b5-109">To set the service endpoints</span></span>
<span data-ttu-id="0f2b5-110">In the **Service Endpoints** dialog, take one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="0f2b5-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="0f2b5-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>
* <span data-ttu-id="0f2b5-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>
* <span data-ttu-id="0f2b5-113">If you want to use a private Azure platform:</span><span class="sxs-lookup"><span data-stu-id="0f2b5-113">If you want to use a private Azure platform:</span></span>
  1. <span data-ttu-id="0f2b5-114">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-114">Click **Edit**.</span></span>
  2. <span data-ttu-id="0f2b5-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="0f2b5-116">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-116">Click **OK**.</span></span>
  3. <span data-ttu-id="0f2b5-117">In the preferencesets.xml file, create a new `preferenceset` element.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="0f2b5-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="0f2b5-119">You can use the values provided for the existing `preferenceset` elements as templates.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="0f2b5-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>
  4. <span data-ttu-id="0f2b5-121">Save and close preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-121">Save and close preferencesets.xml.</span></span>
  5. <span data-ttu-id="0f2b5-122">Reopen the **Service Endpoints** dialog.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-122">Reopen the **Service Endpoints** dialog.</span></span>
  6. <span data-ttu-id="0f2b5-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>
  7. <span data-ttu-id="0f2b5-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="0f2b5-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span><span class="sxs-lookup"><span data-stu-id="0f2b5-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="0f2b5-126">See Also</span><span class="sxs-lookup"><span data-stu-id="0f2b5-126">See Also</span></span>
<span data-ttu-id="0f2b5-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f2b5-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="0f2b5-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f2b5-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="0f2b5-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f2b5-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="0f2b5-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="0f2b5-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->

