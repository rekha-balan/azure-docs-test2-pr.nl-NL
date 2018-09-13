---
title: Azure Active Directory Reporting FAQ | Microsoft Docs
description: Azure Active Directory reporting FAQ.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/18/2017
ms.author: markvi
ms.openlocfilehash: e39ee63d190308b87ebeb43adeb8b3e5db86df57
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551631"
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="a3895-103">Azure Active Directory reporting FAQ</span><span class="sxs-lookup"><span data-stu-id="a3895-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="a3895-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span><span class="sxs-lookup"><span data-stu-id="a3895-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="a3895-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a3895-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="a3895-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="a3895-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="a3895-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span><span class="sxs-lookup"><span data-stu-id="a3895-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="a3895-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="a3895-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="a3895-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span><span class="sxs-lookup"><span data-stu-id="a3895-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="a3895-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span><span class="sxs-lookup"><span data-stu-id="a3895-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="a3895-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span><span class="sxs-lookup"><span data-stu-id="a3895-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="a3895-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span><span class="sxs-lookup"><span data-stu-id="a3895-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="a3895-113">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="a3895-113">**A:** No.</span></span> <span data-ttu-id="a3895-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span><span class="sxs-lookup"><span data-stu-id="a3895-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="a3895-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="a3895-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="a3895-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span><span class="sxs-lookup"><span data-stu-id="a3895-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="a3895-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span><span class="sxs-lookup"><span data-stu-id="a3895-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="a3895-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="a3895-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="a3895-119">**Q: How many records I can download from Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="a3895-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="a3895-120">**A:** You can download up to 120K records from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a3895-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="a3895-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span><span class="sxs-lookup"><span data-stu-id="a3895-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="a3895-122">**Q: How many records can I query through the activities API?**</span><span class="sxs-lookup"><span data-stu-id="a3895-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="a3895-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span><span class="sxs-lookup"><span data-stu-id="a3895-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="a3895-124">If you do use the “top” operator, you can query up to 500K records.</span><span class="sxs-lookup"><span data-stu-id="a3895-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="a3895-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3895-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="a3895-126">**Q: How do I get a premium license?**</span><span class="sxs-lookup"><span data-stu-id="a3895-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="a3895-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span><span class="sxs-lookup"><span data-stu-id="a3895-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="a3895-128">**Q: How soon should I see activities data after getting a premium license?**</span><span class="sxs-lookup"><span data-stu-id="a3895-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="a3895-129">**A:** If you already have activities data as a free license, then you can see the same data.</span><span class="sxs-lookup"><span data-stu-id="a3895-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="a3895-130">If you don’t have any data, then it will take one or two days.</span><span class="sxs-lookup"><span data-stu-id="a3895-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="a3895-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span><span class="sxs-lookup"><span data-stu-id="a3895-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="a3895-132">**A:**: If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span><span class="sxs-lookup"><span data-stu-id="a3895-132">**A:**: If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="a3895-133">When data accumulates, you will see up to 30 days.</span><span class="sxs-lookup"><span data-stu-id="a3895-133">When data accumulates, you will see up to 30 days.</span></span>

 
---

