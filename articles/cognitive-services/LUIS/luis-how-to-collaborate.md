---
title: Collaborate with other contributors on LUIS apps in Azure | Microsoft Docs
description: Learn how to Collaborate with other contributors on Language Understanding (LUIS) applications.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 07/31/2018
ms.author: diberry
ms.openlocfilehash: 99f37cb6dc5e05fc5eb4bde09685435ee57fecc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968643"
---
# <a name="how-to-manage-authors-and-collaborators"></a><span data-ttu-id="4b05e-103">How to manage authors and collaborators</span><span class="sxs-lookup"><span data-stu-id="4b05e-103">How to manage authors and collaborators</span></span> 

<span data-ttu-id="4b05e-104">You can collaborate with others on your LUIS app together.</span><span class="sxs-lookup"><span data-stu-id="4b05e-104">You can collaborate with others on your LUIS app together.</span></span> 

## <a name="owner-and-collaborators"></a><span data-ttu-id="4b05e-105">Owner and collaborators</span><span class="sxs-lookup"><span data-stu-id="4b05e-105">Owner and collaborators</span></span>

<span data-ttu-id="4b05e-106">An app has a single author, the owner, but can have many collaborators.</span><span class="sxs-lookup"><span data-stu-id="4b05e-106">An app has a single author, the owner, but can have many collaborators.</span></span> 

## <a name="add-collaborator"></a><span data-ttu-id="4b05e-107">Add collaborator</span><span class="sxs-lookup"><span data-stu-id="4b05e-107">Add collaborator</span></span>

<span data-ttu-id="4b05e-108">To allow collaborators to edit your LUIS app, on the **Settings** page of your LUIS app, enter the email of the collaborator and click **Add collaborator**.</span><span class="sxs-lookup"><span data-stu-id="4b05e-108">To allow collaborators to edit your LUIS app, on the **Settings** page of your LUIS app, enter the email of the collaborator and click **Add collaborator**.</span></span> <span data-ttu-id="4b05e-109">Collaborators can sign in and edit your LUIS app at the same time you are working on the app.</span><span class="sxs-lookup"><span data-stu-id="4b05e-109">Collaborators can sign in and edit your LUIS app at the same time you are working on the app.</span></span>

![Add collaborator](./media/luis-how-to-collaborate/add-collaborator.png)

## <a name="transfer-of-ownership"></a><span data-ttu-id="4b05e-111">Transfer of ownership</span><span class="sxs-lookup"><span data-stu-id="4b05e-111">Transfer of ownership</span></span>

<span data-ttu-id="4b05e-112">While LUIS doesn't currently support transfer of ownership, you can export your app, and another LUIS user can import the app.</span><span class="sxs-lookup"><span data-stu-id="4b05e-112">While LUIS doesn't currently support transfer of ownership, you can export your app, and another LUIS user can import the app.</span></span> <span data-ttu-id="4b05e-113">There may be minor differences in LUIS scores between the two applications.</span><span class="sxs-lookup"><span data-stu-id="4b05e-113">There may be minor differences in LUIS scores between the two applications.</span></span> 

## <a name="azure-active-directory-tenant-user"></a><span data-ttu-id="4b05e-114">Azure Active Directory tenant user</span><span class="sxs-lookup"><span data-stu-id="4b05e-114">Azure Active Directory tenant user</span></span>

<span data-ttu-id="4b05e-115">LUIS uses standard Azure Active Directory (Azure AD) consent flow.</span><span class="sxs-lookup"><span data-stu-id="4b05e-115">LUIS uses standard Azure Active Directory (Azure AD) consent flow.</span></span> 

<span data-ttu-id="4b05e-116">The tenant admin should work directly with the user who needs access granted to use LUIS in the Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b05e-116">The tenant admin should work directly with the user who needs access granted to use LUIS in the Azure AD.</span></span> 

<span data-ttu-id="4b05e-117">First, the user signs into LUIS, and sees the pop-up dialog needing admin approval.</span><span class="sxs-lookup"><span data-stu-id="4b05e-117">First, the user signs into LUIS, and sees the pop-up dialog needing admin approval.</span></span> <span data-ttu-id="4b05e-118">The user contacts the tenant admin before continuing.</span><span class="sxs-lookup"><span data-stu-id="4b05e-118">The user contacts the tenant admin before continuing.</span></span> 

<span data-ttu-id="4b05e-119">Second, the tenant admin signs into LUIS, and sees a consent flow pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="4b05e-119">Second, the tenant admin signs into LUIS, and sees a consent flow pop-up dialog.</span></span> <span data-ttu-id="4b05e-120">This is the dialog the admin needs to give permission for the user.</span><span class="sxs-lookup"><span data-stu-id="4b05e-120">This is the dialog the admin needs to give permission for the user.</span></span> <span data-ttu-id="4b05e-121">Once the admin accepts the permission, the user is able to continue with LUIS.</span><span class="sxs-lookup"><span data-stu-id="4b05e-121">Once the admin accepts the permission, the user is able to continue with LUIS.</span></span>

<span data-ttu-id="4b05e-122">If the tenant admin will not sign in to LUIS, the admin can access [consent](https://account.activedirectory.windowsazure.com/r#/applications) for LUIS.</span><span class="sxs-lookup"><span data-stu-id="4b05e-122">If the tenant admin will not sign in to LUIS, the admin can access [consent](https://account.activedirectory.windowsazure.com/r#/applications) for LUIS.</span></span> 

![Azure active directory permission by app website](./media/luis-how-to-account-settings/tenant-permissions.png)

<span data-ttu-id="4b05e-124">If the tenant admin only wants certain users to use LUIS, refer to this [identity blog](https://blogs.technet.microsoft.com/tfg/2017/10/15/english-tips-to-manage-azure-ad-users-consent-to-applications-using-azure-ad-graph-api/).</span><span class="sxs-lookup"><span data-stu-id="4b05e-124">If the tenant admin only wants certain users to use LUIS, refer to this [identity blog](https://blogs.technet.microsoft.com/tfg/2017/10/15/english-tips-to-manage-azure-ad-users-consent-to-applications-using-azure-ad-graph-api/).</span></span>

### <a name="user-accounts-with-multiple-emails-for-collaborators"></a><span data-ttu-id="4b05e-125">User accounts with multiple emails for collaborators</span><span class="sxs-lookup"><span data-stu-id="4b05e-125">User accounts with multiple emails for collaborators</span></span>

<span data-ttu-id="4b05e-126">If you add collaborators to a LUIS app, you are specifying the exact email address a collaborator needs to use LUIS as a collaborator.</span><span class="sxs-lookup"><span data-stu-id="4b05e-126">If you add collaborators to a LUIS app, you are specifying the exact email address a collaborator needs to use LUIS as a collaborator.</span></span> <span data-ttu-id="4b05e-127">While Azure Active Directory (Azure AD) allows a single user to have more than one email account used interchangeably, LUIS requires the user to sign in with the email address specified in the collaborator's list.</span><span class="sxs-lookup"><span data-stu-id="4b05e-127">While Azure Active Directory (Azure AD) allows a single user to have more than one email account used interchangeably, LUIS requires the user to sign in with the email address specified in the collaborator's list.</span></span>