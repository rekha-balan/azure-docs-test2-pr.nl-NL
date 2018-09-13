---
title: How to prepare for an SSL IP address change - Azure
description: If your SSL IP address is going to be changed, learn what to do so that your app continues to work after the change.
services: app-service\web
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service-web
ms.workload: web
ms.topic: article
ms.date: 06/28/2018
ms.author: cephalin
ms.openlocfilehash: e8558b4c3c7dafca8d4fff7e2aae0597a66c031d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871578"
---
# <a name="how-to-prepare-for-an-ssl-ip-address-change"></a><span data-ttu-id="70291-103">How to prepare for an SSL IP address change</span><span class="sxs-lookup"><span data-stu-id="70291-103">How to prepare for an SSL IP address change</span></span>

<span data-ttu-id="70291-104">If you received a notification that the SSL IP address of your Azure App Service app is changing, follow the instructions in this article to release existing SSL IP address and assign a new one.</span><span class="sxs-lookup"><span data-stu-id="70291-104">If you received a notification that the SSL IP address of your Azure App Service app is changing, follow the instructions in this article to release existing SSL IP address and assign a new one.</span></span>

## <a name="release-ssl-ip-addresses-and-assign-new-ones"></a><span data-ttu-id="70291-105">Release SSL IP addresses and assign new ones</span><span class="sxs-lookup"><span data-stu-id="70291-105">Release SSL IP addresses and assign new ones</span></span>

1.  <span data-ttu-id="70291-106">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70291-106">Open the [Azure portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="70291-107">In the left-hand navigation menu, select **App Services**.</span><span class="sxs-lookup"><span data-stu-id="70291-107">In the left-hand navigation menu, select **App Services**.</span></span>

3.  <span data-ttu-id="70291-108">Select your App Service app from the list.</span><span class="sxs-lookup"><span data-stu-id="70291-108">Select your App Service app from the list.</span></span>

4.  <span data-ttu-id="70291-109">Under the **Settings** header, click **SSL settings** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="70291-109">Under the **Settings** header, click **SSL settings** in the left navigation.</span></span>

5. <span data-ttu-id="70291-110">In the SSL bindings section, select the host name record.</span><span class="sxs-lookup"><span data-stu-id="70291-110">In the SSL bindings section, select the host name record.</span></span> <span data-ttu-id="70291-111">In the editor that opens, choose **SNI SSL** on the **SSL Type** drop-down menu and click **Add Binding**.</span><span class="sxs-lookup"><span data-stu-id="70291-111">In the editor that opens, choose **SNI SSL** on the **SSL Type** drop-down menu and click **Add Binding**.</span></span> <span data-ttu-id="70291-112">When you see the operation success message, the existing IP address has been released.</span><span class="sxs-lookup"><span data-stu-id="70291-112">When you see the operation success message, the existing IP address has been released.</span></span>

6.  <span data-ttu-id="70291-113">In the **SSL bindings** section, again select the same host name record with the certificate.</span><span class="sxs-lookup"><span data-stu-id="70291-113">In the **SSL bindings** section, again select the same host name record with the certificate.</span></span> <span data-ttu-id="70291-114">In the editor that opens, this time choose **IP Based SSL** on the **SSL Type** drop-down menu and click **Add Binding**.</span><span class="sxs-lookup"><span data-stu-id="70291-114">In the editor that opens, this time choose **IP Based SSL** on the **SSL Type** drop-down menu and click **Add Binding**.</span></span> <span data-ttu-id="70291-115">When you see the operation success message, you’ve acquired a new IP address.</span><span class="sxs-lookup"><span data-stu-id="70291-115">When you see the operation success message, you’ve acquired a new IP address.</span></span>

7.  <span data-ttu-id="70291-116">If an A record (DNS record pointing directly to your IP address) is configured in your Domain Registration Portal (third party DNS Provider or Azure DNS), replace the existing IP address with the newly generated one.</span><span class="sxs-lookup"><span data-stu-id="70291-116">If an A record (DNS record pointing directly to your IP address) is configured in your Domain Registration Portal (third party DNS Provider or Azure DNS), replace the existing IP address with the newly generated one.</span></span> <span data-ttu-id="70291-117">You can find the new IP address by following the instructions in the next section.</span><span class="sxs-lookup"><span data-stu-id="70291-117">You can find the new IP address by following the instructions in the next section.</span></span>

## <a name="find-the-new-ssl-ip-address-in-the-azure-portal"></a><span data-ttu-id="70291-118">Find the new SSL IP address in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="70291-118">Find the new SSL IP address in the Azure Portal</span></span>

1.  <span data-ttu-id="70291-119">Wait a few minutes, and then open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70291-119">Wait a few minutes, and then open the [Azure portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="70291-120">In the left-hand navigation menu, select **App Services**.</span><span class="sxs-lookup"><span data-stu-id="70291-120">In the left-hand navigation menu, select **App Services**.</span></span>

3.  <span data-ttu-id="70291-121">Select your App Service app from the list.</span><span class="sxs-lookup"><span data-stu-id="70291-121">Select your App Service app from the list.</span></span>

4.  <span data-ttu-id="70291-122">Under the **Settings** header, click **Properties** in the left navigation, and find the section labeled **Virtual IP address**.</span><span class="sxs-lookup"><span data-stu-id="70291-122">Under the **Settings** header, click **Properties** in the left navigation, and find the section labeled **Virtual IP address**.</span></span>

5. <span data-ttu-id="70291-123">Copy the IP address and reconfigure your domain record or IP mechanism.</span><span class="sxs-lookup"><span data-stu-id="70291-123">Copy the IP address and reconfigure your domain record or IP mechanism.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70291-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="70291-124">Next steps</span></span>

<span data-ttu-id="70291-125">This article explained how to prepare for an IP address change that was initiated by Azure.</span><span class="sxs-lookup"><span data-stu-id="70291-125">This article explained how to prepare for an IP address change that was initiated by Azure.</span></span> <span data-ttu-id="70291-126">For more information about IP addresses in Azure App Service, see [SSL and SSL IP addresses in Azure App Service](app-service-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="70291-126">For more information about IP addresses in Azure App Service, see [SSL and SSL IP addresses in Azure App Service](app-service-ip-addresses.md).</span></span>
