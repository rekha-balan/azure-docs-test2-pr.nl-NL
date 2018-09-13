---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 517ebbf739c64c0364dc21386fee86ebc740e997
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45358998"
---
<span data-ttu-id="385fb-103">When you generate a client certificate, it's automatically installed on the computer that you used to generate it.</span><span class="sxs-lookup"><span data-stu-id="385fb-103">When you generate a client certificate, it's automatically installed on the computer that you used to generate it.</span></span> <span data-ttu-id="385fb-104">If you want to install the client certificate on another client computer, you need to export the client certificate that you generated.</span><span class="sxs-lookup"><span data-stu-id="385fb-104">If you want to install the client certificate on another client computer, you need to export the client certificate that you generated.</span></span>

1. <span data-ttu-id="385fb-105">To export a client certificate, open **Manage user certificates**.</span><span class="sxs-lookup"><span data-stu-id="385fb-105">To export a client certificate, open **Manage user certificates**.</span></span> <span data-ttu-id="385fb-106">The client certificates that you generated are, by default, located in 'Certificates - Current User\Personal\Certificates'.</span><span class="sxs-lookup"><span data-stu-id="385fb-106">The client certificates that you generated are, by default, located in 'Certificates - Current User\Personal\Certificates'.</span></span> <span data-ttu-id="385fb-107">Right-click the client certificate that you want to export, click **all tasks**, and then click **Export** to open the **Certificate Export Wizard**.</span><span class="sxs-lookup"><span data-stu-id="385fb-107">Right-click the client certificate that you want to export, click **all tasks**, and then click **Export** to open the **Certificate Export Wizard**.</span></span>

  ![Export](./media/vpn-gateway-certificates-export-client-cert-include/export.png)
2. <span data-ttu-id="385fb-109">In the Certificate Export Wizard, click **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="385fb-109">In the Certificate Export Wizard, click **Next** to continue.</span></span>

  ![Next](./media/vpn-gateway-certificates-export-client-cert-include/next.png)
3. <span data-ttu-id="385fb-111">Select **Yes, export the private key**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="385fb-111">Select **Yes, export the private key**, and then click **Next**.</span></span>

  ![export private key](./media/vpn-gateway-certificates-export-client-cert-include/privatekeyexport.png)
4. <span data-ttu-id="385fb-113">On the **Export File Format** page, leave the defaults selected.</span><span class="sxs-lookup"><span data-stu-id="385fb-113">On the **Export File Format** page, leave the defaults selected.</span></span> <span data-ttu-id="385fb-114">Make sure that **Include all certificates in the certification path if possible** is selected.</span><span class="sxs-lookup"><span data-stu-id="385fb-114">Make sure that **Include all certificates in the certification path if possible** is selected.</span></span> <span data-ttu-id="385fb-115">This setting additionally exports the root certificate information that is required for successful client authentication.</span><span class="sxs-lookup"><span data-stu-id="385fb-115">This setting additionally exports the root certificate information that is required for successful client authentication.</span></span> <span data-ttu-id="385fb-116">Without it, client authentication fails because the client doesn't have the trusted root certificate.</span><span class="sxs-lookup"><span data-stu-id="385fb-116">Without it, client authentication fails because the client doesn't have the trusted root certificate.</span></span> <span data-ttu-id="385fb-117">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="385fb-117">Then, click **Next**.</span></span>

  ![export file format](./media/vpn-gateway-certificates-export-client-cert-include/includeallcerts.png)
5. <span data-ttu-id="385fb-119">On the **Security** page, you must protect the private key.</span><span class="sxs-lookup"><span data-stu-id="385fb-119">On the **Security** page, you must protect the private key.</span></span> <span data-ttu-id="385fb-120">If you select to use a password, make sure to record or remember the password that you set for this certificate.</span><span class="sxs-lookup"><span data-stu-id="385fb-120">If you select to use a password, make sure to record or remember the password that you set for this certificate.</span></span> <span data-ttu-id="385fb-121">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="385fb-121">Then, click **Next**.</span></span>

  ![security](./media/vpn-gateway-certificates-export-client-cert-include/security.png)
6. <span data-ttu-id="385fb-123">On the **File to Export**, **Browse** to the location to which you want to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="385fb-123">On the **File to Export**, **Browse** to the location to which you want to export the certificate.</span></span> <span data-ttu-id="385fb-124">For **File name**, name the certificate file.</span><span class="sxs-lookup"><span data-stu-id="385fb-124">For **File name**, name the certificate file.</span></span> <span data-ttu-id="385fb-125">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="385fb-125">Then, click **Next**.</span></span>

  ![file to export](./media/vpn-gateway-certificates-export-client-cert-include/filetoexport.png)
7. <span data-ttu-id="385fb-127">Click **Finish** to export the certificate.</span><span class="sxs-lookup"><span data-stu-id="385fb-127">Click **Finish** to export the certificate.</span></span>

  ![finish](./media/vpn-gateway-certificates-export-client-cert-include/finish.png)