---
title: Setting Up Named Authentication Credentials | Microsoft Docs
description: 'Learn how to to provide credentials that Visual Studio can use to authenticate requests to Azure to publish an application to Azure from Visual Studio or to monitor an existing cloud service.. '
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: 6a3de01281071698c090569b2ea0ea22ee16ed46
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563813"
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="7de9d-103">Setting Up Named Authentication Credentials</span><span class="sxs-lookup"><span data-stu-id="7de9d-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="7de9d-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span><span class="sxs-lookup"><span data-stu-id="7de9d-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="7de9d-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span><span class="sxs-lookup"><span data-stu-id="7de9d-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="7de9d-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Azure**.</span><span class="sxs-lookup"><span data-stu-id="7de9d-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Azure**.</span></span> <span data-ttu-id="7de9d-107">When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you need to do.</span><span class="sxs-lookup"><span data-stu-id="7de9d-107">When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you need to do.</span></span>

<span data-ttu-id="7de9d-108">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span><span class="sxs-lookup"><span data-stu-id="7de9d-108">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="7de9d-109">This topic describes this method, which is still supported in Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="7de9d-109">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="7de9d-110">The following items are required for authentication to Azure.</span><span class="sxs-lookup"><span data-stu-id="7de9d-110">The following items are required for authentication to Azure.</span></span>

* <span data-ttu-id="7de9d-111">Your subscription ID</span><span class="sxs-lookup"><span data-stu-id="7de9d-111">Your subscription ID</span></span>
* <span data-ttu-id="7de9d-112">A valid X.509 v3 certificate</span><span class="sxs-lookup"><span data-stu-id="7de9d-112">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="7de9d-113">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="7de9d-113">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="7de9d-114">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span><span class="sxs-lookup"><span data-stu-id="7de9d-114">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="7de9d-115">Visual Studio uses your subscription ID together with the certificate data as credentials.</span><span class="sxs-lookup"><span data-stu-id="7de9d-115">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="7de9d-116">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span><span class="sxs-lookup"><span data-stu-id="7de9d-116">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="7de9d-117">The subscription file can contain credentials for more than one subscription.</span><span class="sxs-lookup"><span data-stu-id="7de9d-117">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="7de9d-118">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span><span class="sxs-lookup"><span data-stu-id="7de9d-118">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="7de9d-119">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="7de9d-119">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="7de9d-120">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span><span class="sxs-lookup"><span data-stu-id="7de9d-120">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="modify-or-export-authentication-credentials-in-visual-studio"></a><span data-ttu-id="7de9d-121">Modify or Export Authentication Credentials in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7de9d-121">Modify or Export Authentication Credentials in Visual Studio</span></span>
<span data-ttu-id="7de9d-122">You can also set up, modify, or export your authentication credentials in the **New Subscription** dialog box, which appears if you perform either of the following actions:</span><span class="sxs-lookup"><span data-stu-id="7de9d-122">You can also set up, modify, or export your authentication credentials in the **New Subscription** dialog box, which appears if you perform either of the following actions:</span></span>

* <span data-ttu-id="7de9d-123">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage Subscriptions**, choose the **Certificates** tab, and choose the **New** or **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="7de9d-123">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage Subscriptions**, choose the **Certificates** tab, and choose the **New** or **Edit** button.</span></span>
* <span data-ttu-id="7de9d-124">When you publish an Azure cloud service from the **Publish Azure Application** wizard, choose **Manage** in the **Choose your Subscription** list, then choose the Certificates tab, and then choose the **New** or **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="7de9d-124">When you publish an Azure cloud service from the **Publish Azure Application** wizard, choose **Manage** in the **Choose your Subscription** list, then choose the Certificates tab, and then choose the **New** or **Edit** button.</span></span>

<span data-ttu-id="7de9d-125">The following procedure assumes that the **New Subscription** dialog box is open.</span><span class="sxs-lookup"><span data-stu-id="7de9d-125">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="7de9d-126">To set up authentication credentials in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7de9d-126">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="7de9d-127">In the **Select an existing certificate** for authentication list, choose a certificate.</span><span class="sxs-lookup"><span data-stu-id="7de9d-127">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="7de9d-128">Choose the **Copy the full path** button.</span><span class="sxs-lookup"><span data-stu-id="7de9d-128">Choose the **Copy the full path** button.</span></span> <span data-ttu-id="7de9d-129">The path for the certificate (.cer file) is copied to the Clipboard.</span><span class="sxs-lookup"><span data-stu-id="7de9d-129">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="7de9d-130">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="7de9d-130">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   >
   >
3. <span data-ttu-id="7de9d-131">To upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885):</span><span class="sxs-lookup"><span data-stu-id="7de9d-131">To upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885):</span></span>

   1. <span data-ttu-id="7de9d-132">Choose the Azure Portal link.</span><span class="sxs-lookup"><span data-stu-id="7de9d-132">Choose the Azure Portal link.</span></span>

        <span data-ttu-id="7de9d-133">The [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) opens.</span><span class="sxs-lookup"><span data-stu-id="7de9d-133">The [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) opens.</span></span>
   2. <span data-ttu-id="7de9d-134">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and then choose the **Cloud Services** button.</span><span class="sxs-lookup"><span data-stu-id="7de9d-134">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and then choose the **Cloud Services** button.</span></span>
   3. <span data-ttu-id="7de9d-135">Choose the cloud service that interests you.</span><span class="sxs-lookup"><span data-stu-id="7de9d-135">Choose the cloud service that interests you.</span></span>

       <span data-ttu-id="7de9d-136">The page for the service opens.</span><span class="sxs-lookup"><span data-stu-id="7de9d-136">The page for the service opens.</span></span>
   4. <span data-ttu-id="7de9d-137">On the **Certificates** tab, choose the **Upload** button.</span><span class="sxs-lookup"><span data-stu-id="7de9d-137">On the **Certificates** tab, choose the **Upload** button.</span></span>
   5. <span data-ttu-id="7de9d-138">Paste the full path of the .cer file that you just created, and then enter the password that you specified.</span><span class="sxs-lookup"><span data-stu-id="7de9d-138">Paste the full path of the .cer file that you just created, and then enter the password that you specified.</span></span>
