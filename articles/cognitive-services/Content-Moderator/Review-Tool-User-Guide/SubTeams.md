---
title: Teams and subteams in the Content Moderator API | Microsoft Docs
description: Learn how to use teams and subteams in the Content Moderator API for Cognitive Services.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 06/22/2017
ms.author: sajagtap
ms.openlocfilehash: 161c7cd8bac07d5ffc138297d98a40317a8d88fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828100"
---
# <a name="team-and-subteams"></a><span data-ttu-id="27807-103">Team and Subteams</span><span class="sxs-lookup"><span data-stu-id="27807-103">Team and Subteams</span></span> #

<span data-ttu-id="27807-104">You must create a Team before using Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="27807-104">You must create a Team before using Content Moderator.</span></span> <span data-ttu-id="27807-105">When you sign up and name your team, this team will become your default team.</span><span class="sxs-lookup"><span data-stu-id="27807-105">When you sign up and name your team, this team will become your default team.</span></span> <span data-ttu-id="27807-106">You can only have one team in the Review tool.</span><span class="sxs-lookup"><span data-stu-id="27807-106">You can only have one team in the Review tool.</span></span> <span data-ttu-id="27807-107">However, you can create multiple subteams.</span><span class="sxs-lookup"><span data-stu-id="27807-107">However, you can create multiple subteams.</span></span> <span data-ttu-id="27807-108">Subteams are useful for creating escalation teams or teams dedicated to reviewing specific categories of content.</span><span class="sxs-lookup"><span data-stu-id="27807-108">Subteams are useful for creating escalation teams or teams dedicated to reviewing specific categories of content.</span></span> <span data-ttu-id="27807-109">For example, you may want send adult content to a different team for more review.</span><span class="sxs-lookup"><span data-stu-id="27807-109">For example, you may want send adult content to a different team for more review.</span></span>

<span data-ttu-id="27807-110">This topic explains how to create subteams, and quickly assign reviews on the fly.</span><span class="sxs-lookup"><span data-stu-id="27807-110">This topic explains how to create subteams, and quickly assign reviews on the fly.</span></span> <span data-ttu-id="27807-111">However, you can use [Workflows](workflows.md) to assign reviews based on specific criteria.</span><span class="sxs-lookup"><span data-stu-id="27807-111">However, you can use [Workflows](workflows.md) to assign reviews based on specific criteria.</span></span>

## <a name="go-to-the-teams-setting"></a><span data-ttu-id="27807-112">Go to the Teams Setting</span><span class="sxs-lookup"><span data-stu-id="27807-112">Go to the Teams Setting</span></span> ##

<span data-ttu-id="27807-113">To get started on creating a subteam, select the **Teams** option under Settings.</span><span class="sxs-lookup"><span data-stu-id="27807-113">To get started on creating a subteam, select the **Teams** option under Settings.</span></span>

![Team Settings](images/0-teams-1.png)

## <a name="create-subteams"></a><span data-ttu-id="27807-115">Create subteams</span><span class="sxs-lookup"><span data-stu-id="27807-115">Create subteams</span></span> ##

<span data-ttu-id="27807-116">The Default team contains all potential reviewers; subteams are subsets of the default team.</span><span class="sxs-lookup"><span data-stu-id="27807-116">The Default team contains all potential reviewers; subteams are subsets of the default team.</span></span> <span data-ttu-id="27807-117">You cannot assign someone to a subteam if they are not already members of the default team, so you need to add any reviewers to the default team now.</span><span class="sxs-lookup"><span data-stu-id="27807-117">You cannot assign someone to a subteam if they are not already members of the default team, so you need to add any reviewers to the default team now.</span></span> <span data-ttu-id="27807-118">Click the Invite button on the Team page.</span><span class="sxs-lookup"><span data-stu-id="27807-118">Click the Invite button on the Team page.</span></span>

![Invite users](images/invite-users.png)

### <a name="1-create-a-subteam"></a><span data-ttu-id="27807-120">1. Create a subteam.</span><span class="sxs-lookup"><span data-stu-id="27807-120">1. Create a subteam.</span></span>
<span data-ttu-id="27807-121">Scroll down the Team page to the Subteam section.</span><span class="sxs-lookup"><span data-stu-id="27807-121">Scroll down the Team page to the Subteam section.</span></span> <span data-ttu-id="27807-122">Click the Add Subteam button.</span><span class="sxs-lookup"><span data-stu-id="27807-122">Click the Add Subteam button.</span></span> 

![Add Subteam](images/1-teams-1.png)

### <a name="2-name-your-subteam"></a><span data-ttu-id="27807-124">2. Name your subteam.</span><span class="sxs-lookup"><span data-stu-id="27807-124">2. Name your subteam.</span></span>
<span data-ttu-id="27807-125">Enter your subteam name in the dialog, then click Save.</span><span class="sxs-lookup"><span data-stu-id="27807-125">Enter your subteam name in the dialog, then click Save.</span></span>

![Subteam Name](images/1-Teams-2.PNG)

### <a name="3-assign-members-from-your-default-team"></a><span data-ttu-id="27807-127">3. Assign members from your default team.</span><span class="sxs-lookup"><span data-stu-id="27807-127">3. Assign members from your default team.</span></span>
<span data-ttu-id="27807-128">Click the Add Member button to assign members from your default team to one or more subteams.</span><span class="sxs-lookup"><span data-stu-id="27807-128">Click the Add Member button to assign members from your default team to one or more subteams.</span></span> <span data-ttu-id="27807-129">You can only add existing users to a subteam.</span><span class="sxs-lookup"><span data-stu-id="27807-129">You can only add existing users to a subteam.</span></span> <span data-ttu-id="27807-130">For adding new users who are not in the review tool, invite them by using the "Invite" button on the Team Settings page.</span><span class="sxs-lookup"><span data-stu-id="27807-130">For adding new users who are not in the review tool, invite them by using the "Invite" button on the Team Settings page.</span></span>

![Assign subteam members](images/1-Teams-3.PNG)

## <a name="assign-reviews-to-your-subteams"></a><span data-ttu-id="27807-132">Assign reviews to your subteams</span><span class="sxs-lookup"><span data-stu-id="27807-132">Assign reviews to your subteams</span></span> ##

<span data-ttu-id="27807-133">Once you have your subteams created and team members assigned, you can start assigning image and text reviews to those subteams.</span><span class="sxs-lookup"><span data-stu-id="27807-133">Once you have your subteams created and team members assigned, you can start assigning image and text reviews to those subteams.</span></span> <span data-ttu-id="27807-134">This is done from the Review window.</span><span class="sxs-lookup"><span data-stu-id="27807-134">This is done from the Review window.</span></span>
<span data-ttu-id="27807-135">If you want to assign an individual image to a subteam, click the ellipsis in the upper-right corner of the image, select Move to, and select a subteam.</span><span class="sxs-lookup"><span data-stu-id="27807-135">If you want to assign an individual image to a subteam, click the ellipsis in the upper-right corner of the image, select Move to, and select a subteam.</span></span>

![Assign image review to subteam](images/3-review-image-subteam-1.png)

## <a name="switch-between-subteams-to-review-assigned-content"></a><span data-ttu-id="27807-137">Switch between subteams to review assigned content</span><span class="sxs-lookup"><span data-stu-id="27807-137">Switch between subteams to review assigned content</span></span> ##

<span data-ttu-id="27807-138">If you are a member of one or more subteams, you can switch between those subteams from the Review Tools Dashboard.</span><span class="sxs-lookup"><span data-stu-id="27807-138">If you are a member of one or more subteams, you can switch between those subteams from the Review Tools Dashboard.</span></span> <span data-ttu-id="27807-139">To see all of the current pending reviews belonging to a subteam, select Choose Subteam from the Image tab.</span><span class="sxs-lookup"><span data-stu-id="27807-139">To see all of the current pending reviews belonging to a subteam, select Choose Subteam from the Image tab.</span></span>

![Switch between subteams](images/3-review-image-subteam-2.png)
