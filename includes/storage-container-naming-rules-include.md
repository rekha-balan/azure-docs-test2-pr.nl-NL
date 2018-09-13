<span data-ttu-id="56db9-101">Every blob in Azure storage must reside in a container.</span><span class="sxs-lookup"><span data-stu-id="56db9-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="56db9-102">The container forms part of the blob name.</span><span class="sxs-lookup"><span data-stu-id="56db9-102">The container forms part of the blob name.</span></span> <span data-ttu-id="56db9-103">For example, `mycontainer` is the name of the container in these sample blob URIs:</span><span class="sxs-lookup"><span data-stu-id="56db9-103">For example, `mycontainer` is the name of the container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="56db9-104">A container name must be a valid DNS name, conforming to the following naming rules:</span><span class="sxs-lookup"><span data-stu-id="56db9-104">A container name must be a valid DNS name, conforming to the following naming rules:</span></span>

1. <span data-ttu-id="56db9-105">Container names must start with a letter or number, and can contain only letters, numbers, and the dash (-) character.</span><span class="sxs-lookup"><span data-stu-id="56db9-105">Container names must start with a letter or number, and can contain only letters, numbers, and the dash (-) character.</span></span>
2. <span data-ttu-id="56db9-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span><span class="sxs-lookup"><span data-stu-id="56db9-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="56db9-107">All letters in a container name must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="56db9-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="56db9-108">Container names must be from 3 through 63 characters long.</span><span class="sxs-lookup"><span data-stu-id="56db9-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56db9-109">Note that the name of a container must always be lowercase.</span><span class="sxs-lookup"><span data-stu-id="56db9-109">Note that the name of a container must always be lowercase.</span></span> <span data-ttu-id="56db9-110">If you include an upper-case letter in a container name, or otherwise violate the container naming rules, you may receive a 400 error (Bad Request).</span><span class="sxs-lookup"><span data-stu-id="56db9-110">If you include an upper-case letter in a container name, or otherwise violate the container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

