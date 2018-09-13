---
title: Customer data request features in Azure IoT Central | Microsoft Docs
description: Customer data request features in Azure IoT Central
author: dominicbetts
ms.author: dobett
ms.date: 05/17/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: timlt
ms.openlocfilehash: bb5e263b0332f957b4e7f4a928ccd53f639bcd9c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868554"
---
# <a name="summary-of-customer-data-request-features"></a><span data-ttu-id="aaa61-103">Summary of customer data request features</span><span class="sxs-lookup"><span data-stu-id="aaa61-103">Summary of customer data request features</span></span>

<span data-ttu-id="aaa61-104">Azure IoT Central is a fully managed Internet of Things (IoT) software-as-a-service solution that makes it easy to connect, monitor, and manage your IoT assets at scale, create deep insights from your IoT data, and take informed action.</span><span class="sxs-lookup"><span data-stu-id="aaa61-104">Azure IoT Central is a fully managed Internet of Things (IoT) software-as-a-service solution that makes it easy to connect, monitor, and manage your IoT assets at scale, create deep insights from your IoT data, and take informed action.</span></span>

[!INCLUDE [gdpr-intro-sentence](../../includes/gdpr-intro-sentence.md)]

## <a name="identifying-customer-data"></a><span data-ttu-id="aaa61-105">Identifying customer data</span><span class="sxs-lookup"><span data-stu-id="aaa61-105">Identifying customer data</span></span>

<span data-ttu-id="aaa61-106">Azure Active Directory Object-IDs are used to identify users and assign roles.</span><span class="sxs-lookup"><span data-stu-id="aaa61-106">Azure Active Directory Object-IDs are used to identify users and assign roles.</span></span> <span data-ttu-id="aaa61-107">The Azure IoT Central portal displays user email addresses for role assignments but only the Azure Active Directory Object-ID is stored, the email address is dynamically queried from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aaa61-107">The Azure IoT Central portal displays user email addresses for role assignments but only the Azure Active Directory Object-ID is stored, the email address is dynamically queried from Azure Active Directory.</span></span> <span data-ttu-id="aaa61-108">Azure IoT Central administrators can view, export, and delete application users in the user administration section of an Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="aaa61-108">Azure IoT Central administrators can view, export, and delete application users in the user administration section of an Azure IoT Central application.</span></span>

<span data-ttu-id="aaa61-109">Within the application, email addresses can be configured to receive alerts.</span><span class="sxs-lookup"><span data-stu-id="aaa61-109">Within the application, email addresses can be configured to receive alerts.</span></span> <span data-ttu-id="aaa61-110">In this case, email addresses are stored within IoT Central and must be managed from the in-app account administration page.</span><span class="sxs-lookup"><span data-stu-id="aaa61-110">In this case, email addresses are stored within IoT Central and must be managed from the in-app account administration page.</span></span>

<span data-ttu-id="aaa61-111">Regarding devices, Microsoft maintains no information and has no access to data that enables  device to user correlation.</span><span class="sxs-lookup"><span data-stu-id="aaa61-111">Regarding devices, Microsoft maintains no information and has no access to data that enables  device to user correlation.</span></span> <span data-ttu-id="aaa61-112">Many of the devices managed in Azure IoT Central are not personal devices, for example a vending machine or coffee maker.</span><span class="sxs-lookup"><span data-stu-id="aaa61-112">Many of the devices managed in Azure IoT Central are not personal devices, for example a vending machine or coffee maker.</span></span> <span data-ttu-id="aaa61-113">Customers may, however, consider some devices to be personally identifiable and at their discretion may maintain their own asset or inventory tracking systems that tie devices to individuals.</span><span class="sxs-lookup"><span data-stu-id="aaa61-113">Customers may, however, consider some devices to be personally identifiable and at their discretion may maintain their own asset or inventory tracking systems that tie devices to individuals.</span></span> <span data-ttu-id="aaa61-114">Azure IoT Central manages and stores all data associated with devices as if it were personal data.</span><span class="sxs-lookup"><span data-stu-id="aaa61-114">Azure IoT Central manages and stores all data associated with devices as if it were personal data.</span></span>

<span data-ttu-id="aaa61-115">When you use Microsoft enterprise services, Microsoft generates some information, known as system-generated logs.</span><span class="sxs-lookup"><span data-stu-id="aaa61-115">When you use Microsoft enterprise services, Microsoft generates some information, known as system-generated logs.</span></span> <span data-ttu-id="aaa61-116">These logs constitute factual actions conducted within the service and diagnostic data related to individual devices, and are not related to user activity.</span><span class="sxs-lookup"><span data-stu-id="aaa61-116">These logs constitute factual actions conducted within the service and diagnostic data related to individual devices, and are not related to user activity.</span></span> <span data-ttu-id="aaa61-117">Azure IoT Central system-generated logs are not accessible or exportable by application administrators.</span><span class="sxs-lookup"><span data-stu-id="aaa61-117">Azure IoT Central system-generated logs are not accessible or exportable by application administrators.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="aaa61-118">Deleting customer data</span><span class="sxs-lookup"><span data-stu-id="aaa61-118">Deleting customer data</span></span>

<span data-ttu-id="aaa61-119">The ability to delete user data is only provided through the IoT Central administration page.</span><span class="sxs-lookup"><span data-stu-id="aaa61-119">The ability to delete user data is only provided through the IoT Central administration page.</span></span> <span data-ttu-id="aaa61-120">Application administrators can select the user to be deleted and click **Delete** in the upper right corner of the application to delete the record.</span><span class="sxs-lookup"><span data-stu-id="aaa61-120">Application administrators can select the user to be deleted and click **Delete** in the upper right corner of the application to delete the record.</span></span> <span data-ttu-id="aaa61-121">Application administrators can also remove individual accounts that are no longer associated with the application in question.</span><span class="sxs-lookup"><span data-stu-id="aaa61-121">Application administrators can also remove individual accounts that are no longer associated with the application in question.</span></span>

<span data-ttu-id="aaa61-122">After a user is deleted, no further alerts are emailed to them.</span><span class="sxs-lookup"><span data-stu-id="aaa61-122">After a user is deleted, no further alerts are emailed to them.</span></span> <span data-ttu-id="aaa61-123">However, their email address must be individually removed from each configured alert.</span><span class="sxs-lookup"><span data-stu-id="aaa61-123">However, their email address must be individually removed from each configured alert.</span></span>

<span data-ttu-id="aaa61-124">For more information, see [Configure rules and actions for your device](tutorial-configure-rules.md).</span><span class="sxs-lookup"><span data-stu-id="aaa61-124">For more information, see [Configure rules and actions for your device](tutorial-configure-rules.md).</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="aaa61-125">Exporting customer data</span><span class="sxs-lookup"><span data-stu-id="aaa61-125">Exporting customer data</span></span>

<span data-ttu-id="aaa61-126">The ability to export data is only provided through the IoT Central administration page.</span><span class="sxs-lookup"><span data-stu-id="aaa61-126">The ability to export data is only provided through the IoT Central administration page.</span></span> <span data-ttu-id="aaa61-127">Customer data, including assigned roles, can be selected, copied, and pasted by an application administrator.</span><span class="sxs-lookup"><span data-stu-id="aaa61-127">Customer data, including assigned roles, can be selected, copied, and pasted by an application administrator.</span></span>

## <a name="links-to-additional-documentation"></a><span data-ttu-id="aaa61-128">Links to additional documentation</span><span class="sxs-lookup"><span data-stu-id="aaa61-128">Links to additional documentation</span></span>

<span data-ttu-id="aaa61-129">For more information about account administration, including role definitions, see [How to administer your application](howto-administer.md).</span><span class="sxs-lookup"><span data-stu-id="aaa61-129">For more information about account administration, including role definitions, see [How to administer your application](howto-administer.md).</span></span>
