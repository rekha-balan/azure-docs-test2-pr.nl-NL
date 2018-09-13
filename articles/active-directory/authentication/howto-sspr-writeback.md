---
title: How-to configure password writeback for Azure AD SSPR
description: Use Azure AD and Azure AD Connect to writeback passwords to an on-premises directory
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: e613ff742096077fe1765d4b855b6c7d409cc228
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857575"
---
# <a name="how-to-configure-password-writeback"></a><span data-ttu-id="9d5c4-103">How-to: Configure password writeback</span><span class="sxs-lookup"><span data-stu-id="9d5c4-103">How-to: Configure password writeback</span></span>

<span data-ttu-id="9d5c4-104">We recommend that you use the auto-update feature of [Azure AD Connect](./../connect/active-directory-aadconnect-get-started-express.md) when using password writeback.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-104">We recommend that you use the auto-update feature of [Azure AD Connect](./../connect/active-directory-aadconnect-get-started-express.md) when using password writeback.</span></span>

<span data-ttu-id="9d5c4-105">The following steps assume you have already configured Azure AD Connect in your environment by using the [Express](./../connect/active-directory-aadconnect-get-started-express.md) or [Custom](./../connect/active-directory-aadconnect-get-started-custom.md) settings.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-105">The following steps assume you have already configured Azure AD Connect in your environment by using the [Express](./../connect/active-directory-aadconnect-get-started-express.md) or [Custom](./../connect/active-directory-aadconnect-get-started-custom.md) settings.</span></span>

1. <span data-ttu-id="9d5c4-106">To configure and enable password writeback, sign in to your Azure AD Connect server and start the **Azure AD Connect** configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-106">To configure and enable password writeback, sign in to your Azure AD Connect server and start the **Azure AD Connect** configuration wizard.</span></span>
2. <span data-ttu-id="9d5c4-107">On the **Welcome** page, select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-107">On the **Welcome** page, select **Configure**.</span></span>
3. <span data-ttu-id="9d5c4-108">On the **Additional tasks** page, select **Customize synchronization options**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-108">On the **Additional tasks** page, select **Customize synchronization options**, and then select **Next**.</span></span>
4. <span data-ttu-id="9d5c4-109">On the **Connect to Azure AD** page, enter a global administrator credential, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-109">On the **Connect to Azure AD** page, enter a global administrator credential, and then select **Next**.</span></span>
5. <span data-ttu-id="9d5c4-110">On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-110">On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.</span></span>
6. <span data-ttu-id="9d5c4-111">On the **Optional features** page, select the box next to **Password writeback** and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-111">On the **Optional features** page, select the box next to **Password writeback** and select **Next**.</span></span>
   <span data-ttu-id="9d5c4-112">![Enable password writeback in Azure AD Connect][Writeback]</span><span class="sxs-lookup"><span data-stu-id="9d5c4-112">![Enable password writeback in Azure AD Connect][Writeback]</span></span>
7. <span data-ttu-id="9d5c4-113">On the **Ready to configure** page, select **Configure** and wait for the process to finish.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-113">On the **Ready to configure** page, select **Configure** and wait for the process to finish.</span></span>
8. <span data-ttu-id="9d5c4-114">When you see the configuration finish, select **Exit**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-114">When you see the configuration finish, select **Exit**.</span></span>

<span data-ttu-id="9d5c4-115">For common troubleshooting tasks related to password writeback, see the section [Troubleshoot password writeback](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) in our troubleshooting article.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-115">For common troubleshooting tasks related to password writeback, see the section [Troubleshoot password writeback](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) in our troubleshooting article.</span></span>

## <a name="active-directory-permissions"></a><span data-ttu-id="9d5c4-116">Active Directory permissions</span><span class="sxs-lookup"><span data-stu-id="9d5c4-116">Active Directory permissions</span></span>

<span data-ttu-id="9d5c4-117">The account specified in the Azure AD Connect utility must have the following items set if you want to be in scope for SSPR:</span><span class="sxs-lookup"><span data-stu-id="9d5c4-117">The account specified in the Azure AD Connect utility must have the following items set if you want to be in scope for SSPR:</span></span>

* <span data-ttu-id="9d5c4-118">**Reset password**</span><span class="sxs-lookup"><span data-stu-id="9d5c4-118">**Reset password**</span></span> 
* <span data-ttu-id="9d5c4-119">**Change password**</span><span class="sxs-lookup"><span data-stu-id="9d5c4-119">**Change password**</span></span> 
* <span data-ttu-id="9d5c4-120">**Write permissions** on `lockoutTime`</span><span class="sxs-lookup"><span data-stu-id="9d5c4-120">**Write permissions** on `lockoutTime`</span></span>
* <span data-ttu-id="9d5c4-121">**Write permissions** on `pwdLastSet`</span><span class="sxs-lookup"><span data-stu-id="9d5c4-121">**Write permissions** on `pwdLastSet`</span></span>
* <span data-ttu-id="9d5c4-122">**Extended rights** on either:</span><span class="sxs-lookup"><span data-stu-id="9d5c4-122">**Extended rights** on either:</span></span>
   * <span data-ttu-id="9d5c4-123">The root object of *each domain* in that forest</span><span class="sxs-lookup"><span data-stu-id="9d5c4-123">The root object of *each domain* in that forest</span></span>
   * <span data-ttu-id="9d5c4-124">The user organizational units (OUs) you want to be in scope for SSPR</span><span class="sxs-lookup"><span data-stu-id="9d5c4-124">The user organizational units (OUs) you want to be in scope for SSPR</span></span>

<span data-ttu-id="9d5c4-125">If you're not sure what account the described account refers to, open the Azure Active Directory Connect configuration UI and select the **View current configuration** option.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-125">If you're not sure what account the described account refers to, open the Azure Active Directory Connect configuration UI and select the **View current configuration** option.</span></span> <span data-ttu-id="9d5c4-126">The account that you need to add permission to is listed under **Synchronized Directories**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-126">The account that you need to add permission to is listed under **Synchronized Directories**.</span></span>

<span data-ttu-id="9d5c4-127">If you set these permissions, the MA service account for each forest can manage passwords on behalf of the user accounts within that forest.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-127">If you set these permissions, the MA service account for each forest can manage passwords on behalf of the user accounts within that forest.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9d5c4-128">If you neglect to assign these permissions, then, even though writeback appears to be configured correctly, users will encounter errors when they attempt to manage their on-premises passwords from the cloud.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-128">If you neglect to assign these permissions, then, even though writeback appears to be configured correctly, users will encounter errors when they attempt to manage their on-premises passwords from the cloud.</span></span>
>

> [!NOTE]
> <span data-ttu-id="9d5c4-129">It might take up to an hour or more for these permissions to replicate to all the objects in your directory.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-129">It might take up to an hour or more for these permissions to replicate to all the objects in your directory.</span></span>
>

<span data-ttu-id="9d5c4-130">To set up the appropriate permissions for password writeback to occur, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="9d5c4-130">To set up the appropriate permissions for password writeback to occur, complete the following steps:</span></span>

1. <span data-ttu-id="9d5c4-131">Open Active Directory Users and Computers with an account that has the appropriate domain administration permissions.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-131">Open Active Directory Users and Computers with an account that has the appropriate domain administration permissions.</span></span>
2. <span data-ttu-id="9d5c4-132">From the **View** menu, make sure **Advanced features** is turned on.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-132">From the **View** menu, make sure **Advanced features** is turned on.</span></span>
3. <span data-ttu-id="9d5c4-133">In the left panel, right-click the object that represents the root of the domain and select **Properties** > **Security** > **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-133">In the left panel, right-click the object that represents the root of the domain and select **Properties** > **Security** > **Advanced**.</span></span>
4. <span data-ttu-id="9d5c4-134">From the **Permissions** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-134">From the **Permissions** tab, select **Add**.</span></span>
5. <span data-ttu-id="9d5c4-135">Pick the account that permissions are being applied to (from the Azure AD Connect setup).</span><span class="sxs-lookup"><span data-stu-id="9d5c4-135">Pick the account that permissions are being applied to (from the Azure AD Connect setup).</span></span>
6. <span data-ttu-id="9d5c4-136">In the **Applies to** drop-down list, select **Descendent user** objects.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-136">In the **Applies to** drop-down list, select **Descendent user** objects.</span></span>
7. <span data-ttu-id="9d5c4-137">Under **Permissions**, select the boxes for the following:</span><span class="sxs-lookup"><span data-stu-id="9d5c4-137">Under **Permissions**, select the boxes for the following:</span></span>
    * <span data-ttu-id="9d5c4-138">**Reset password**</span><span class="sxs-lookup"><span data-stu-id="9d5c4-138">**Reset password**</span></span>
    * <span data-ttu-id="9d5c4-139">**Change password**</span><span class="sxs-lookup"><span data-stu-id="9d5c4-139">**Change password**</span></span>
    * <span data-ttu-id="9d5c4-140">**Write lockoutTime**</span><span class="sxs-lookup"><span data-stu-id="9d5c4-140">**Write lockoutTime**</span></span>
    * <span data-ttu-id="9d5c4-141">**Write pwdLastSet**</span><span class="sxs-lookup"><span data-stu-id="9d5c4-141">**Write pwdLastSet**</span></span>
8. <span data-ttu-id="9d5c4-142">Select **Apply/OK** to apply the changes and exit any open dialog boxes.</span><span class="sxs-lookup"><span data-stu-id="9d5c4-142">Select **Apply/OK** to apply the changes and exit any open dialog boxes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d5c4-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d5c4-143">Next steps</span></span>

[<span data-ttu-id="9d5c4-144">What is password writeback?</span><span class="sxs-lookup"><span data-stu-id="9d5c4-144">What is password writeback?</span></span>](concept-sspr-writeback.md)

[Writeback]: ./media/howto-sspr-writeback/enablepasswordwriteback.png "Enable password writeback in Azure AD Connect"
