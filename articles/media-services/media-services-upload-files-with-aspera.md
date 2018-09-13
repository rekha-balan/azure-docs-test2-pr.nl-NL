---
title: Upload files into an Azure Media Services account using Aspera | Microsoft Docs
description: This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.
services: media-services
documentationcenter: ''
author: johndeu
manager: erikre
editor: ''
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 3ec8e83aaba126e2175f580e197f08a15eac38b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550180"
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="92131-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span><span class="sxs-lookup"><span data-stu-id="92131-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="92131-104">Overview</span><span class="sxs-lookup"><span data-stu-id="92131-104">Overview</span></span>

<span data-ttu-id="92131-105">**Aspera** is a high-speed file transfer software.</span><span class="sxs-lookup"><span data-stu-id="92131-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="92131-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span><span class="sxs-lookup"><span data-stu-id="92131-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="92131-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span><span class="sxs-lookup"><span data-stu-id="92131-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="92131-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="92131-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="92131-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="92131-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="92131-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span><span class="sxs-lookup"><span data-stu-id="92131-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="92131-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="92131-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="92131-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span><span class="sxs-lookup"><span data-stu-id="92131-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="92131-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span><span class="sxs-lookup"><span data-stu-id="92131-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="92131-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="92131-114">Prerequisites</span></span> 

<span data-ttu-id="92131-115">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="92131-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="92131-116">A Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="92131-116">A Windows Live ID</span></span>
* <span data-ttu-id="92131-117">An [Azure account](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="92131-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="92131-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92131-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="92131-119">An [Azure Media Services account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="92131-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="92131-120">Purchase Aspera On Demand for Azure</span><span class="sxs-lookup"><span data-stu-id="92131-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="92131-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span><span class="sxs-lookup"><span data-stu-id="92131-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="92131-122">Search for Aspera and select 'Server On Demand'.</span><span class="sxs-lookup"><span data-stu-id="92131-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="92131-124">Review the subscription plans and click on 'Sign Up'</span><span class="sxs-lookup"><span data-stu-id="92131-124">Review the subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="92131-126">Fill in the specifics for your Server on Demand subscription.</span><span class="sxs-lookup"><span data-stu-id="92131-126">Fill in the specifics for your Server on Demand subscription.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="92131-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span><span class="sxs-lookup"><span data-stu-id="92131-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span></span> <span data-ttu-id="92131-129">In the **Plan details** panel, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="92131-129">In the **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="92131-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="92131-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="92131-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span><span class="sxs-lookup"><span data-stu-id="92131-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span></span> <span data-ttu-id="92131-133">Once you have reviewed the legal terms, click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="92131-133">Once you have reviewed the legal terms, click **Purchase**.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="92131-135">Complete the purchase by clicking **Create**.</span><span class="sxs-lookup"><span data-stu-id="92131-135">Complete the purchase by clicking **Create**.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="92131-137">The Azure dashboard will announce that it is provisioning the service.</span><span class="sxs-lookup"><span data-stu-id="92131-137">The Azure dashboard will announce that it is provisioning the service.</span></span>  <span data-ttu-id="92131-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span><span class="sxs-lookup"><span data-stu-id="92131-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span></span> <span data-ttu-id="92131-139">Once you have found the service, double click on it to launch the service management portal.</span><span class="sxs-lookup"><span data-stu-id="92131-139">Once you have found the service, double click on it to launch the service management portal.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="92131-141">Launch the Aspera management portal.</span><span class="sxs-lookup"><span data-stu-id="92131-141">Launch the Aspera management portal.</span></span> <span data-ttu-id="92131-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span><span class="sxs-lookup"><span data-stu-id="92131-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span></span>  <span data-ttu-id="92131-143">A new panel will be launched.</span><span class="sxs-lookup"><span data-stu-id="92131-143">A new panel will be launched.</span></span> <span data-ttu-id="92131-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span><span class="sxs-lookup"><span data-stu-id="92131-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span></span>  <span data-ttu-id="92131-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span><span class="sxs-lookup"><span data-stu-id="92131-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="92131-146">Once you click on the resource name, another panel is launched.</span><span class="sxs-lookup"><span data-stu-id="92131-146">Once you click on the resource name, another panel is launched.</span></span> <span data-ttu-id="92131-147">In that newly launched panel, you will see a 'Manage' link.</span><span class="sxs-lookup"><span data-stu-id="92131-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="92131-148">Click on the 'Manage' link to launch the Aspera management portal.</span><span class="sxs-lookup"><span data-stu-id="92131-148">Click on the 'Manage' link to launch the Aspera management portal.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="92131-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span><span class="sxs-lookup"><span data-stu-id="92131-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span></span>

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="92131-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span><span class="sxs-lookup"><span data-stu-id="92131-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span></span>

    <span data-ttu-id="92131-153">The following screenshot shows the access creation.</span><span class="sxs-lookup"><span data-stu-id="92131-153">The following screenshot shows the access creation.</span></span> 

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="92131-155">The following screenshot shows the usage reporting interfaces in the portal.</span><span class="sxs-lookup"><span data-stu-id="92131-155">The following screenshot shows the usage reporting interfaces in the portal.</span></span> 

   ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="92131-157">Upload files with Aspera</span><span class="sxs-lookup"><span data-stu-id="92131-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="92131-158">Download and install the Aspera client software:</span><span class="sxs-lookup"><span data-stu-id="92131-158">Download and install the Aspera client software:</span></span>
    
    * [<span data-ttu-id="92131-159">Browser plugin</span><span class="sxs-lookup"><span data-stu-id="92131-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="92131-160">Rich client</span><span class="sxs-lookup"><span data-stu-id="92131-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="92131-161">Make your first transfer.</span><span class="sxs-lookup"><span data-stu-id="92131-161">Make your first transfer.</span></span> <span data-ttu-id="92131-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span><span class="sxs-lookup"><span data-stu-id="92131-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span></span> 

    1. <span data-ttu-id="92131-163">Create an access key, using the Aspera portal.</span><span class="sxs-lookup"><span data-stu-id="92131-163">Create an access key, using the Aspera portal.</span></span>  
    2. <span data-ttu-id="92131-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span><span class="sxs-lookup"><span data-stu-id="92131-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="92131-165">Please read the Aspera client guide for configuration information.</span><span class="sxs-lookup"><span data-stu-id="92131-165">Please read the Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="92131-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="92131-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="92131-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span><span class="sxs-lookup"><span data-stu-id="92131-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span></span> 

        * <span data-ttu-id="92131-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span><span class="sxs-lookup"><span data-stu-id="92131-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span></span>
        * <span data-ttu-id="92131-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span><span class="sxs-lookup"><span data-stu-id="92131-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span></span> 

    <span data-ttu-id="92131-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span><span class="sxs-lookup"><span data-stu-id="92131-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span></span>

    ![Aspera](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="92131-172">Resources</span><span class="sxs-lookup"><span data-stu-id="92131-172">Resources</span></span>

<span data-ttu-id="92131-173">The following resources were mentioned in this article.</span><span class="sxs-lookup"><span data-stu-id="92131-173">The following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="92131-174">Connect Browser Plugin</span><span class="sxs-lookup"><span data-stu-id="92131-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="92131-175">Connect Guide</span><span class="sxs-lookup"><span data-stu-id="92131-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="92131-176">Aspera Client</span><span class="sxs-lookup"><span data-stu-id="92131-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="92131-177">Client Guide</span><span class="sxs-lookup"><span data-stu-id="92131-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="92131-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="92131-178">Next steps</span></span>

<span data-ttu-id="92131-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="92131-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="92131-180">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="92131-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="92131-181">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="92131-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]













