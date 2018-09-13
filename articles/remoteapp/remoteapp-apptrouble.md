---
title: Azure RemoteApp Troubleshooting - Application launch and connection failures  | Microsoft Docs
description: Learn how to troubleshoot issues with starting and connecting to applications in Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cdf0a2133bd50048fb441d49c62cb1508858f31c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564685"
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a><span data-ttu-id="5bae5-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span><span class="sxs-lookup"><span data-stu-id="5bae5-103">Troubleshoot Azure RemoteApp - Application launch and connection failures</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5bae5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="5bae5-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5bae5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="5bae5-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5bae5-106">Applications hosted in Azure RemoteApp can fail to launch for a few different reasons.</span><span class="sxs-lookup"><span data-stu-id="5bae5-106">Applications hosted in Azure RemoteApp can fail to launch for a few different reasons.</span></span> <span data-ttu-id="5bae5-107">This article describes various reasons and error messages users might receive when trying to launch applications.</span><span class="sxs-lookup"><span data-stu-id="5bae5-107">This article describes various reasons and error messages users might receive when trying to launch applications.</span></span> <span data-ttu-id="5bae5-108">It also talks about connection failures.</span><span class="sxs-lookup"><span data-stu-id="5bae5-108">It also talks about connection failures.</span></span> <span data-ttu-id="5bae5-109">(But this article does not describe issues when signing into the Azure RemoteApp client.)</span><span class="sxs-lookup"><span data-stu-id="5bae5-109">(But this article does not describe issues when signing into the Azure RemoteApp client.)</span></span>  

<span data-ttu-id="5bae5-110">Read on for information about common error messages due to app launch and connection failures.</span><span class="sxs-lookup"><span data-stu-id="5bae5-110">Read on for information about common error messages due to app launch and connection failures.</span></span>

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a><span data-ttu-id="5bae5-111">We're getting you set up... Try again in 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="5bae5-111">We're getting you set up... Try again in 10 minutes.</span></span>
<span data-ttu-id="5bae5-112">This error means Azure RemoteApp is scaling up to meet the capacity need of your users.</span><span class="sxs-lookup"><span data-stu-id="5bae5-112">This error means Azure RemoteApp is scaling up to meet the capacity need of your users.</span></span> <span data-ttu-id="5bae5-113">In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users.</span><span class="sxs-lookup"><span data-stu-id="5bae5-113">In the background more Azure RemoteApp VM instances are being created to handle the capacity needs of your users.</span></span> <span data-ttu-id="5bae5-114">Typically this takes around five minutes but can take up to 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="5bae5-114">Typically this takes around five minutes but can take up to 10 minutes.</span></span> <span data-ttu-id="5bae5-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span><span class="sxs-lookup"><span data-stu-id="5bae5-115">Sometimes, this doesn't happen fast enough and resources are needed immediately.</span></span> <span data-ttu-id="5bae5-116">For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time.</span><span class="sxs-lookup"><span data-stu-id="5bae5-116">For example a 9 AM scenario where many users need to use your app in Azure RemoteAppn at the same time.</span></span> <span data-ttu-id="5bae5-117">If this happens to you we can enable **capacity mode** on the back end.</span><span class="sxs-lookup"><span data-stu-id="5bae5-117">If this happens to you we can enable **capacity mode** on the back end.</span></span> <span data-ttu-id="5bae5-118">To do this open an Azure Support ticket.</span><span class="sxs-lookup"><span data-stu-id="5bae5-118">To do this open an Azure Support ticket.</span></span> <span data-ttu-id="5bae5-119">Be certain to include your subscription ID in the request.</span><span class="sxs-lookup"><span data-stu-id="5bae5-119">Be certain to include your subscription ID in the request.</span></span>  

![We are getting you set up](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a><span data-ttu-id="5bae5-121">Could not auto-reconnect to your applications, please re-launch your application</span><span class="sxs-lookup"><span data-stu-id="5bae5-121">Could not auto-reconnect to your applications, please re-launch your application</span></span>
<span data-ttu-id="5bae5-122">This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.</span><span class="sxs-lookup"><span data-stu-id="5bae5-122">This error message is often seen if you were using Azure RemoteApp and then put your PC to sleep longer than 4 hours and then woke your PC up and the Azure RemoteApp client attempt to auto reconnect and timeout was exceeded.</span></span>  <span data-ttu-id="5bae5-123">Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.</span><span class="sxs-lookup"><span data-stu-id="5bae5-123">Instruct users to navigate back to the application and attempt to open it from the Azure RemoteApp client.</span></span>

![Could not auto-reconnect to your applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a><span data-ttu-id="5bae5-125">Problems with the temp profile</span><span class="sxs-lookup"><span data-stu-id="5bae5-125">Problems with the temp profile</span></span>
<span data-ttu-id="5bae5-126">This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.</span><span class="sxs-lookup"><span data-stu-id="5bae5-126">This error occurs when your user profile (User Profile Disk) failed to mount and the user received a temporary profile.</span></span>  <span data-ttu-id="5bae5-127">Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user.</span><span class="sxs-lookup"><span data-stu-id="5bae5-127">Administrators should navigate to the collection in the Azure portal and then go to the **Sessions** tab and attempt to **Log Off** the user.</span></span> <span data-ttu-id="5bae5-128">This will force a full log off of the user session - then have the user attempt to launch an app again.</span><span class="sxs-lookup"><span data-stu-id="5bae5-128">This will force a full log off of the user session - then have the user attempt to launch an app again.</span></span> <span data-ttu-id="5bae5-129">If that fails contact Azure support.</span><span class="sxs-lookup"><span data-stu-id="5bae5-129">If that fails contact Azure support.</span></span>

## <a name="azure-remoteapp-has-stopped-working"></a><span data-ttu-id="5bae5-130">Azure RemoteApp has stopped working</span><span class="sxs-lookup"><span data-stu-id="5bae5-130">Azure RemoteApp has stopped working</span></span>
<span data-ttu-id="5bae5-131">This error message means the Azure RemoteApp client is having an issue and needs to be restarted.</span><span class="sxs-lookup"><span data-stu-id="5bae5-131">This error message means the Azure RemoteApp client is having an issue and needs to be restarted.</span></span> <span data-ttu-id="5bae5-132">Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.</span><span class="sxs-lookup"><span data-stu-id="5bae5-132">Instruct users to close: select **Close program** and then launch the Azure RemoteApp client again.</span></span>  <span data-ttu-id="5bae5-133">If the issue continues open and Azure Support ticket.</span><span class="sxs-lookup"><span data-stu-id="5bae5-133">If the issue continues open and Azure Support ticket.</span></span>

![Azure RemoteApp has stopped working](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a><span data-ttu-id="5bae5-135">An error occurred while Remote Desktop Connection was accessing this resource.</span><span class="sxs-lookup"><span data-stu-id="5bae5-135">An error occurred while Remote Desktop Connection was accessing this resource.</span></span> <span data-ttu-id="5bae5-136">Retry the connection or contact your system administrator</span><span class="sxs-lookup"><span data-stu-id="5bae5-136">Retry the connection or contact your system administrator</span></span>
<span data-ttu-id="5bae5-137">This is a generic error message - contact Azure support so we can investigate.</span><span class="sxs-lookup"><span data-stu-id="5bae5-137">This is a generic error message - contact Azure support so we can investigate.</span></span> 

![Generic Azure RemoteApp message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/remoteapp/media/remoteapp-apptrouble/ra-apptrouble4.png) 





