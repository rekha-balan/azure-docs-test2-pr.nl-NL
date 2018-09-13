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
ms.openlocfilehash: f860a0cebefaebe16c40abf008bd24e333eb80d5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856043"
---
<span data-ttu-id="60934-103">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span><span class="sxs-lookup"><span data-stu-id="60934-103">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="60934-104">When installing a client certificate, you need the password that was created when the client certificate was exported.</span><span class="sxs-lookup"><span data-stu-id="60934-104">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span>

1. <span data-ttu-id="60934-105">Locate and copy the *.pfx* file to the client computer.</span><span class="sxs-lookup"><span data-stu-id="60934-105">Locate and copy the *.pfx* file to the client computer.</span></span> <span data-ttu-id="60934-106">On the client computer, double-click the *.pfx* file to install.</span><span class="sxs-lookup"><span data-stu-id="60934-106">On the client computer, double-click the *.pfx* file to install.</span></span> <span data-ttu-id="60934-107">Leave the **Store Location** as **Current User**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60934-107">Leave the **Store Location** as **Current User**, and then click **Next**.</span></span>
2. <span data-ttu-id="60934-108">On the **File** to import page, don't make any changes.</span><span class="sxs-lookup"><span data-stu-id="60934-108">On the **File** to import page, don't make any changes.</span></span> <span data-ttu-id="60934-109">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60934-109">Click **Next**.</span></span>
3. <span data-ttu-id="60934-110">On the **Private key protection** page, input the password for the certificate, or verify that the security principal is correct, then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60934-110">On the **Private key protection** page, input the password for the certificate, or verify that the security principal is correct, then click **Next**.</span></span>
4. <span data-ttu-id="60934-111">On the **Certificate Store** page, leave the default location, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="60934-111">On the **Certificate Store** page, leave the default location, and then click **Next**.</span></span>
5. <span data-ttu-id="60934-112">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="60934-112">Click **Finish**.</span></span> <span data-ttu-id="60934-113">On the **Security Warning** for the certificate installation, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="60934-113">On the **Security Warning** for the certificate installation, click **Yes**.</span></span> <span data-ttu-id="60934-114">You can feel comfortable clicking 'Yes' because you generated the certificate.</span><span class="sxs-lookup"><span data-stu-id="60934-114">You can feel comfortable clicking 'Yes' because you generated the certificate.</span></span> <span data-ttu-id="60934-115">The certificate is now successfully imported.</span><span class="sxs-lookup"><span data-stu-id="60934-115">The certificate is now successfully imported.</span></span>