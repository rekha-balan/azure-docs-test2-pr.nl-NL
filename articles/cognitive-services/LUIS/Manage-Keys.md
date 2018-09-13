---
title: Manage your keys in LUIS | Microsoft Docs
description: Use Language Understanding Intelligent Services (LUIS) to manage your programmatic API, endpoint, and external keys.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: aadc26ed79eefad53254c043cbb5394844138615
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552881"
---
# <a name="manage-your-keys"></a><span data-ttu-id="f5013-103">Manage your keys</span><span class="sxs-lookup"><span data-stu-id="f5013-103">Manage your keys</span></span>
<span data-ttu-id="f5013-104">A key is your passport to the server allowing you to publish your app to be used by end users.</span><span class="sxs-lookup"><span data-stu-id="f5013-104">A key is your passport to the server allowing you to publish your app to be used by end users.</span></span> <span data-ttu-id="f5013-105">LUIS has three different types of keys:</span><span class="sxs-lookup"><span data-stu-id="f5013-105">LUIS has three different types of keys:</span></span>

* <span data-ttu-id="f5013-106">**Programmatic API Key:** Created automatically per LUIS account and you don't have to buy it.</span><span class="sxs-lookup"><span data-stu-id="f5013-106">**Programmatic API Key:** Created automatically per LUIS account and you don't have to buy it.</span></span> <span data-ttu-id="f5013-107">It enables you to author and edit your application using LUIS programmatic APIs.</span><span class="sxs-lookup"><span data-stu-id="f5013-107">It enables you to author and edit your application using LUIS programmatic APIs.</span></span> 
<span data-ttu-id="f5013-108">[Click here for a complete API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f).</span><span class="sxs-lookup"><span data-stu-id="f5013-108">[Click here for a complete API Reference](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f).</span></span>

* <span data-ttu-id="f5013-109">**Endpoint Key(s):** You need to buy it from Microsoft Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5013-109">**Endpoint Key(s):** You need to buy it from Microsoft Azure portal.</span></span> <span data-ttu-id="f5013-110">It is essential for publishing your app and accessing your HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="f5013-110">It is essential for publishing your app and accessing your HTTP endpoint.</span></span> <span data-ttu-id="f5013-111">This key reflects your quota of endpoint hits based on the usage plan you specified while creating the key.</span><span class="sxs-lookup"><span data-stu-id="f5013-111">This key reflects your quota of endpoint hits based on the usage plan you specified while creating the key.</span></span> 

* <span data-ttu-id="f5013-112">**External Key(s):** You need to buy an external key only if you want to use any external services with LUIS (e.g. Bing Spell Check service).</span><span class="sxs-lookup"><span data-stu-id="f5013-112">**External Key(s):** You need to buy an external key only if you want to use any external services with LUIS (e.g. Bing Spell Check service).</span></span>
 
<span data-ttu-id="f5013-113">The process of creating and using endpoint and external keys involves the following tasks in the same order:</span><span class="sxs-lookup"><span data-stu-id="f5013-113">The process of creating and using endpoint and external keys involves the following tasks in the same order:</span></span>

 1. <span data-ttu-id="f5013-114">Create a key on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5013-114">Create a key on Azure portal.</span></span>
 
 2. <span data-ttu-id="f5013-115">Add the key to your LUIS account (on **My Keys** page).</span><span class="sxs-lookup"><span data-stu-id="f5013-115">Add the key to your LUIS account (on **My Keys** page).</span></span> 
 3. <span data-ttu-id="f5013-116">Assign the key to your app on the **Publish** page.</span><span class="sxs-lookup"><span data-stu-id="f5013-116">Assign the key to your app on the **Publish** page.</span></span> 


## <a name="reset-programmatic-api-key"></a><span data-ttu-id="f5013-117">Reset Programmatic API key</span><span class="sxs-lookup"><span data-stu-id="f5013-117">Reset Programmatic API key</span></span>
<span data-ttu-id="f5013-118">You can reset your Programmatic API key to get a new one generated for your account.</span><span class="sxs-lookup"><span data-stu-id="f5013-118">You can reset your Programmatic API key to get a new one generated for your account.</span></span>

<span data-ttu-id="f5013-119">**To reset a Programmatic API key:**</span><span class="sxs-lookup"><span data-stu-id="f5013-119">**To reset a Programmatic API key:**</span></span>

1. <span data-ttu-id="f5013-120">Click **My Keys** on LUIS top navigation bar to access **My Keys** page.</span><span class="sxs-lookup"><span data-stu-id="f5013-120">Click **My Keys** on LUIS top navigation bar to access **My Keys** page.</span></span>

    ![My Keys page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/MyKeys.JPG)
2. <span data-ttu-id="f5013-122">At the top of **My Keys** page, you can see your current Programmatic API key.</span><span class="sxs-lookup"><span data-stu-id="f5013-122">At the top of **My Keys** page, you can see your current Programmatic API key.</span></span> <span data-ttu-id="f5013-123">Click **Reset Programmatic API Key**.</span><span class="sxs-lookup"><span data-stu-id="f5013-123">Click **Reset Programmatic API Key**.</span></span> <span data-ttu-id="f5013-124">The new key will be generated replacing the existing one.</span><span class="sxs-lookup"><span data-stu-id="f5013-124">The new key will be generated replacing the existing one.</span></span>


## <a name="create-and-use-endpoint-keys-for-your-apps"></a><span data-ttu-id="f5013-125">Create and use endpoint keys for your apps</span><span class="sxs-lookup"><span data-stu-id="f5013-125">Create and use endpoint keys for your apps</span></span>
<span data-ttu-id="f5013-126">You can create as many endpoint keys as you need for your LUIS apps on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5013-126">You can create as many endpoint keys as you need for your LUIS apps on Azure portal.</span></span> <span data-ttu-id="f5013-127">These keys will be used for publishing your apps to the Web.</span><span class="sxs-lookup"><span data-stu-id="f5013-127">These keys will be used for publishing your apps to the Web.</span></span>

<span data-ttu-id="f5013-128">**To create an endpoint key on Azure portal:**</span><span class="sxs-lookup"><span data-stu-id="f5013-128">**To create an endpoint key on Azure portal:**</span></span>

1.  <span data-ttu-id="f5013-129">Click **My Keys** on LUIS top navigation bar to access **My Keys** page.</span><span class="sxs-lookup"><span data-stu-id="f5013-129">Click **My Keys** on LUIS top navigation bar to access **My Keys** page.</span></span>

2. <span data-ttu-id="f5013-130">On **My Keys** page, **Endpoint Keys** tab, click **Buy Key on Azure**.</span><span class="sxs-lookup"><span data-stu-id="f5013-130">On **My Keys** page, **Endpoint Keys** tab, click **Buy Key on Azure**.</span></span> <span data-ttu-id="f5013-131">This will take you directly to Microsoft Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5013-131">This will take you directly to Microsoft Azure portal.</span></span> <span data-ttu-id="f5013-132">You can create one or more keys per account by subscribing to one or more subscription tiers.</span><span class="sxs-lookup"><span data-stu-id="f5013-132">You can create one or more keys per account by subscribing to one or more subscription tiers.</span></span> 
3. <span data-ttu-id="f5013-133">For further instructions, see [Creating a subscription key via Azure Ibiza](AzureIbizaSubscription.md).</span><span class="sxs-lookup"><span data-stu-id="f5013-133">For further instructions, see [Creating a subscription key via Azure Ibiza](AzureIbizaSubscription.md).</span></span>

<span data-ttu-id="f5013-134">**To add the endpoint key to your LUIS account:**</span><span class="sxs-lookup"><span data-stu-id="f5013-134">**To add the endpoint key to your LUIS account:**</span></span>

1. <span data-ttu-id="f5013-135">On **My Keys** page, **Endpoint Keys** tab, click **Add a new key**.</span><span class="sxs-lookup"><span data-stu-id="f5013-135">On **My Keys** page, **Endpoint Keys** tab, click **Add a new key**.</span></span>
 
    ![Add Azure key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/MyKeys-AddKey.JPG)
2. <span data-ttu-id="f5013-137">Copy the key you created in Azure portal in the previous procedure and paste it in the **Key Value** text box.</span><span class="sxs-lookup"><span data-stu-id="f5013-137">Copy the key you created in Azure portal in the previous procedure and paste it in the **Key Value** text box.</span></span> 
3. <span data-ttu-id="f5013-138">You can optionally type a name for the key in **Key Name**, for example "Tier1" , and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5013-138">You can optionally type a name for the key in **Key Name**, for example "Tier1" , and then click **Save**.</span></span> <span data-ttu-id="f5013-139">The key will be added to the keys list.</span><span class="sxs-lookup"><span data-stu-id="f5013-139">The key will be added to the keys list.</span></span>

    ![My Keys List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/MyKeys-Keylist.JPG)

<span data-ttu-id="f5013-141">In the list of added keys, you can edit a key name, or delete a key (if no longer needed).</span><span class="sxs-lookup"><span data-stu-id="f5013-141">In the list of added keys, you can edit a key name, or delete a key (if no longer needed).</span></span> <span data-ttu-id="f5013-142">To do this, click the edit</span><span class="sxs-lookup"><span data-stu-id="f5013-142">To do this, click the edit</span></span> ![Edit Key Name button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Rename-Intent-btn.JPG) <span data-ttu-id="f5013-144">or delete button</span><span class="sxs-lookup"><span data-stu-id="f5013-144">or delete button</span></span> ![Delete Key button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) <span data-ttu-id="f5013-146">corresponding to that key in the list.</span><span class="sxs-lookup"><span data-stu-id="f5013-146">corresponding to that key in the list.</span></span>

<span data-ttu-id="f5013-147">**To assign the endpoint key to your app:**</span><span class="sxs-lookup"><span data-stu-id="f5013-147">**To assign the endpoint key to your app:**</span></span>

1. <span data-ttu-id="f5013-148">Access the **Publish** page by clicking **Publish App** on the left panel.</span><span class="sxs-lookup"><span data-stu-id="f5013-148">Access the **Publish** page by clicking **Publish App** on the left panel.</span></span>

2. <span data-ttu-id="f5013-149">From the **Endpoint Key** list, select the key that you want to assign to the app.</span><span class="sxs-lookup"><span data-stu-id="f5013-149">From the **Endpoint Key** list, select the key that you want to assign to the app.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="f5013-150">Whenever you assign a key to the app, an updated endpoint URL will be generated.</span><span class="sxs-lookup"><span data-stu-id="f5013-150">Whenever you assign a key to the app, an updated endpoint URL will be generated.</span></span> <span data-ttu-id="f5013-151">Remember to use the updated endpoint URL in your code.</span><span class="sxs-lookup"><span data-stu-id="f5013-151">Remember to use the updated endpoint URL in your code.</span></span>


## <a name="create-and-use-external-keys"></a><span data-ttu-id="f5013-152">Create and use external keys</span><span class="sxs-lookup"><span data-stu-id="f5013-152">Create and use external keys</span></span>
<span data-ttu-id="f5013-153">External keys are the keys required for any external services that you want to use with your LUIS app to enhance the language understanding experience.</span><span class="sxs-lookup"><span data-stu-id="f5013-153">External keys are the keys required for any external services that you want to use with your LUIS app to enhance the language understanding experience.</span></span> <span data-ttu-id="f5013-154">One of these services, which is currently available, is [Bing Spell Check](https://www.microsoft.com/cognitive-services/en-us/bing-spell-check-api/documentation).</span><span class="sxs-lookup"><span data-stu-id="f5013-154">One of these services, which is currently available, is [Bing Spell Check](https://www.microsoft.com/cognitive-services/en-us/bing-spell-check-api/documentation).</span></span> <span data-ttu-id="f5013-155">It can be used with LUIS to detect and correct any spelling mistakes in end-user queries submitted to your application's endpoint.</span><span class="sxs-lookup"><span data-stu-id="f5013-155">It can be used with LUIS to detect and correct any spelling mistakes in end-user queries submitted to your application's endpoint.</span></span>

<span data-ttu-id="f5013-156">**To create and add an external key to your LUIS account:**</span><span class="sxs-lookup"><span data-stu-id="f5013-156">**To create and add an external key to your LUIS account:**</span></span>

1. <span data-ttu-id="f5013-157">On **My Keys** page, **External Keys**, click **Add a new key**.</span><span class="sxs-lookup"><span data-stu-id="f5013-157">On **My Keys** page, **External Keys**, click **Add a new key**.</span></span> <span data-ttu-id="f5013-158">The following dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="f5013-158">The following dialog box appears.</span></span>

    ![Add a new external key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/MyKeys-AddExternal.JPG)
2. <span data-ttu-id="f5013-160">From the **Key Type** list, select "BingSpellCheck".</span><span class="sxs-lookup"><span data-stu-id="f5013-160">From the **Key Type** list, select "BingSpellCheck".</span></span>
3. <span data-ttu-id="f5013-161">Copy the key you created on Azure and paste it in **Key Value**, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5013-161">Copy the key you created on Azure and paste it in **Key Value**, and then click **Save**.</span></span> <span data-ttu-id="f5013-162">The key will be added to the keys list.</span><span class="sxs-lookup"><span data-stu-id="f5013-162">The key will be added to the keys list.</span></span>


<span data-ttu-id="f5013-163">**To assign the external key to your app:**</span><span class="sxs-lookup"><span data-stu-id="f5013-163">**To assign the external key to your app:**</span></span>

1. <span data-ttu-id="f5013-164">Access the **Publish** page by clicking **Publish App** on the left panel.</span><span class="sxs-lookup"><span data-stu-id="f5013-164">Access the **Publish** page by clicking **Publish App** on the left panel.</span></span>
2. <span data-ttu-id="f5013-165">Click **Add Key Association** ![Add Key Association button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/MyKeys-AddKeyAssociation-btn.JPG).</span><span class="sxs-lookup"><span data-stu-id="f5013-165">Click **Add Key Association** ![Add Key Association button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/MyKeys-AddKeyAssociation-btn.JPG).</span></span>

3. <span data-ttu-id="f5013-166">Select Bing Spell Check as the key type from the **Key Type** list, and select from the **Key Value** list the external key that you want to assign to the app.</span><span class="sxs-lookup"><span data-stu-id="f5013-166">Select Bing Spell Check as the key type from the **Key Type** list, and select from the **Key Value** list the external key that you want to assign to the app.</span></span> 







