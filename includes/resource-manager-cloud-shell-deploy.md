## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="0a6be-101">Deploy template from Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0a6be-101">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="0a6be-102">You can use [Cloud Shell](../articles/cloud-shell/overview.md) to deploy your template.</span><span class="sxs-lookup"><span data-stu-id="0a6be-102">You can use [Cloud Shell](../articles/cloud-shell/overview.md) to deploy your template.</span></span> <span data-ttu-id="0a6be-103">However, you must first load your template into the storage account for your Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0a6be-103">However, you must first load your template into the storage account for your Cloud Shell.</span></span> <span data-ttu-id="0a6be-104">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../articles/cloud-shell/overview.md) for information about setting it up.</span><span class="sxs-lookup"><span data-stu-id="0a6be-104">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../articles/cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="0a6be-105">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a6be-105">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="0a6be-106">Select your Cloud Shell resource group.</span><span class="sxs-lookup"><span data-stu-id="0a6be-106">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="0a6be-107">The name pattern is `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="0a6be-107">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Select resource group](./media/resource-manager-cloud-shell-deploy/select-cs-resource-group.png)

1. <span data-ttu-id="0a6be-109">Select the storage account for your Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0a6be-109">Select the storage account for your Cloud Shell.</span></span>

   ![Select storage account](./media/resource-manager-cloud-shell-deploy/select-storage.png)

1. <span data-ttu-id="0a6be-111">Select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="0a6be-111">Select **Blobs**.</span></span>

   ![Select blobs](./media/resource-manager-cloud-shell-deploy/select-blobs.png)

1. <span data-ttu-id="0a6be-113">Select **+ Container**.</span><span class="sxs-lookup"><span data-stu-id="0a6be-113">Select **+ Container**.</span></span>

   ![Add container](./media/resource-manager-cloud-shell-deploy/add-container.png)

1. <span data-ttu-id="0a6be-115">Give your container a name and an access level.</span><span class="sxs-lookup"><span data-stu-id="0a6be-115">Give your container a name and an access level.</span></span> <span data-ttu-id="0a6be-116">The sample template in this article contains no sensitive information, so allow anonymous read access.</span><span class="sxs-lookup"><span data-stu-id="0a6be-116">The sample template in this article contains no sensitive information, so allow anonymous read access.</span></span> <span data-ttu-id="0a6be-117">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a6be-117">Select **OK**.</span></span>

   ![Provide container values](./media/resource-manager-cloud-shell-deploy/provide-container-values.png)

1. <span data-ttu-id="0a6be-119">Select the container you created.</span><span class="sxs-lookup"><span data-stu-id="0a6be-119">Select the container you created.</span></span>

   ![Select new container](./media/resource-manager-cloud-shell-deploy/select-container.png)

1. <span data-ttu-id="0a6be-121">Select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="0a6be-121">Select **Upload**.</span></span>

   ![Upload blob](./media/resource-manager-cloud-shell-deploy/upload-blob.png)

1. <span data-ttu-id="0a6be-123">Find and upload your template.</span><span class="sxs-lookup"><span data-stu-id="0a6be-123">Find and upload your template.</span></span>

   ![Upload file](./media/resource-manager-cloud-shell-deploy/find-and-upload-template.png)

1. <span data-ttu-id="0a6be-125">After it has uploaded, select the template.</span><span class="sxs-lookup"><span data-stu-id="0a6be-125">After it has uploaded, select the template.</span></span>

   ![Select new template](./media/resource-manager-cloud-shell-deploy/select-new-template.png)

1. <span data-ttu-id="0a6be-127">Copy the URL.</span><span class="sxs-lookup"><span data-stu-id="0a6be-127">Copy the URL.</span></span>

   ![Copy URL](./media/resource-manager-cloud-shell-deploy/copy-url.png)

1. <span data-ttu-id="0a6be-129">Open the prompt.</span><span class="sxs-lookup"><span data-stu-id="0a6be-129">Open the prompt.</span></span>

   ![Open Cloud Shell](./media/resource-manager-cloud-shell-deploy/start-cloud-shell.png)
