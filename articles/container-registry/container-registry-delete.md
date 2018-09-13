---
title: Delete image resources in Azure Container Registry
description: Details on how to effectively manage registry size by deleting container image data.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 07/27/2018
ms.author: marsma
ms.openlocfilehash: 6ab667a01eddd84d1145868a3ae499e7497035c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868592"
---
# <a name="delete-container-images-in-azure-container-registry"></a><span data-ttu-id="3effd-103">Delete container images in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="3effd-103">Delete container images in Azure Container Registry</span></span>

<span data-ttu-id="3effd-104">To maintain the size of your Azure container registry, you should periodically delete stale image data.</span><span class="sxs-lookup"><span data-stu-id="3effd-104">To maintain the size of your Azure container registry, you should periodically delete stale image data.</span></span> <span data-ttu-id="3effd-105">While some container images deployed into production may require longer-term storage, others can typically be deleted more quickly.</span><span class="sxs-lookup"><span data-stu-id="3effd-105">While some container images deployed into production may require longer-term storage, others can typically be deleted more quickly.</span></span> <span data-ttu-id="3effd-106">For example, in an automated build and test scenario, your registry can quickly fill with images that might never be deployed, and can be purged shortly after completing the build and test pass.</span><span class="sxs-lookup"><span data-stu-id="3effd-106">For example, in an automated build and test scenario, your registry can quickly fill with images that might never be deployed, and can be purged shortly after completing the build and test pass.</span></span>

<span data-ttu-id="3effd-107">Because you can delete image data in several different ways, it's important to understand how each delete operation affects storage usage.</span><span class="sxs-lookup"><span data-stu-id="3effd-107">Because you can delete image data in several different ways, it's important to understand how each delete operation affects storage usage.</span></span> <span data-ttu-id="3effd-108">This article first introduces the components of a Docker registry and container images, then covers several methods for deleting image data.</span><span class="sxs-lookup"><span data-stu-id="3effd-108">This article first introduces the components of a Docker registry and container images, then covers several methods for deleting image data.</span></span>

## <a name="registry"></a><span data-ttu-id="3effd-109">Registry</span><span class="sxs-lookup"><span data-stu-id="3effd-109">Registry</span></span>

<span data-ttu-id="3effd-110">A container *registry* is a service that stores and distributes container images.</span><span class="sxs-lookup"><span data-stu-id="3effd-110">A container *registry* is a service that stores and distributes container images.</span></span> <span data-ttu-id="3effd-111">Docker Hub is a public Docker container registry, while Azure Container Registry provides private Docker container registries in Azure.</span><span class="sxs-lookup"><span data-stu-id="3effd-111">Docker Hub is a public Docker container registry, while Azure Container Registry provides private Docker container registries in Azure.</span></span>

## <a name="repository"></a><span data-ttu-id="3effd-112">Repository</span><span class="sxs-lookup"><span data-stu-id="3effd-112">Repository</span></span>

<span data-ttu-id="3effd-113">Container registries manage *repositories*, collections of container images with the same name, but different tags.</span><span class="sxs-lookup"><span data-stu-id="3effd-113">Container registries manage *repositories*, collections of container images with the same name, but different tags.</span></span> <span data-ttu-id="3effd-114">For example, the following three images are in the "acr-helloworld" repository:</span><span class="sxs-lookup"><span data-stu-id="3effd-114">For example, the following three images are in the "acr-helloworld" repository:</span></span>

```
acr-helloworld:latest
acr-helloworld:v1
acr-helloworld:v2
```

<span data-ttu-id="3effd-115">Repository names can also include [namespaces](container-registry-best-practices.md#repository-namespaces).</span><span class="sxs-lookup"><span data-stu-id="3effd-115">Repository names can also include [namespaces](container-registry-best-practices.md#repository-namespaces).</span></span> <span data-ttu-id="3effd-116">Namespaces allow you group images using forward slash-delimited repository names, for example:</span><span class="sxs-lookup"><span data-stu-id="3effd-116">Namespaces allow you group images using forward slash-delimited repository names, for example:</span></span>

```
marketing/campaign10-18/web:v2
marketing/campaign10-18/api:v3
marketing/campaign10-18/email-sender:v2
product-returns/web-submission:20180604
product-returns/legacy-integrator:20180715
```

## <a name="components-of-an-image"></a><span data-ttu-id="3effd-117">Components of an image</span><span class="sxs-lookup"><span data-stu-id="3effd-117">Components of an image</span></span>

<span data-ttu-id="3effd-118">A container image within a registry is associated with one or more tags, has one or more layers, and is identified by a manifest.</span><span class="sxs-lookup"><span data-stu-id="3effd-118">A container image within a registry is associated with one or more tags, has one or more layers, and is identified by a manifest.</span></span> <span data-ttu-id="3effd-119">Understanding how these components relate to each other can help you determine the best method for freeing space in your registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-119">Understanding how these components relate to each other can help you determine the best method for freeing space in your registry.</span></span>

### <a name="tag"></a><span data-ttu-id="3effd-120">Tag</span><span class="sxs-lookup"><span data-stu-id="3effd-120">Tag</span></span>

<span data-ttu-id="3effd-121">An image's *tag* specifies its version.</span><span class="sxs-lookup"><span data-stu-id="3effd-121">An image's *tag* specifies its version.</span></span> <span data-ttu-id="3effd-122">A single image within a repository can be assigned one or many tags, and may also be "untagged."</span><span class="sxs-lookup"><span data-stu-id="3effd-122">A single image within a repository can be assigned one or many tags, and may also be "untagged."</span></span> <span data-ttu-id="3effd-123">That is, you can delete all tags from an image, while the image's data (its layers) remain the registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-123">That is, you can delete all tags from an image, while the image's data (its layers) remain the registry.</span></span>

<span data-ttu-id="3effd-124">The repository (or repository and namespace) plus a tag defines an image's name.</span><span class="sxs-lookup"><span data-stu-id="3effd-124">The repository (or repository and namespace) plus a tag defines an image's name.</span></span> <span data-ttu-id="3effd-125">You can push and pull an image by specifying its name in the push or pull operation.</span><span class="sxs-lookup"><span data-stu-id="3effd-125">You can push and pull an image by specifying its name in the push or pull operation.</span></span>

<span data-ttu-id="3effd-126">In a private registry like Azure Container Registry, the image name also includes the fully qualified name of the registry host.</span><span class="sxs-lookup"><span data-stu-id="3effd-126">In a private registry like Azure Container Registry, the image name also includes the fully qualified name of the registry host.</span></span> <span data-ttu-id="3effd-127">The registry host for images in ACR is in the format *acrname.azurecr.io*.</span><span class="sxs-lookup"><span data-stu-id="3effd-127">The registry host for images in ACR is in the format *acrname.azurecr.io*.</span></span> <span data-ttu-id="3effd-128">For example, the full name of the first image in the 'marketing' namespace in the previous section would be:</span><span class="sxs-lookup"><span data-stu-id="3effd-128">For example, the full name of the first image in the 'marketing' namespace in the previous section would be:</span></span>

```
myregistry.azurecr.io/marketing/campaign10-18/web:v2
```

<span data-ttu-id="3effd-129">For a discussion on image tagging best practices, see the [Docker Tagging: Best practices for tagging and versioning docker images][tagging-best-practices] blog post on MSDN.</span><span class="sxs-lookup"><span data-stu-id="3effd-129">For a discussion on image tagging best practices, see the [Docker Tagging: Best practices for tagging and versioning docker images][tagging-best-practices] blog post on MSDN.</span></span>

### <a name="layer"></a><span data-ttu-id="3effd-130">Layer</span><span class="sxs-lookup"><span data-stu-id="3effd-130">Layer</span></span>

<span data-ttu-id="3effd-131">Images are made up of one or more *layers*, each corresponding to a line in the Dockerfile that defines the image.</span><span class="sxs-lookup"><span data-stu-id="3effd-131">Images are made up of one or more *layers*, each corresponding to a line in the Dockerfile that defines the image.</span></span> <span data-ttu-id="3effd-132">Images in a registry share common layers, increasing storage efficiency.</span><span class="sxs-lookup"><span data-stu-id="3effd-132">Images in a registry share common layers, increasing storage efficiency.</span></span> <span data-ttu-id="3effd-133">For example, several images in different repositories might share the same Alpine Linux base layer, but only one copy of that layer is stored in the registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-133">For example, several images in different repositories might share the same Alpine Linux base layer, but only one copy of that layer is stored in the registry.</span></span>

<span data-ttu-id="3effd-134">Layer sharing also optimizes layer distribution to nodes with multiple images sharing common layers.</span><span class="sxs-lookup"><span data-stu-id="3effd-134">Layer sharing also optimizes layer distribution to nodes with multiple images sharing common layers.</span></span> <span data-ttu-id="3effd-135">For example, if an image already on a node includes the Alpine Linux layer as its base, the subsequent pull of a different image referencing the same layer doesn't transfer the layer to the node.</span><span class="sxs-lookup"><span data-stu-id="3effd-135">For example, if an image already on a node includes the Alpine Linux layer as its base, the subsequent pull of a different image referencing the same layer doesn't transfer the layer to the node.</span></span> <span data-ttu-id="3effd-136">Instead, it references the layer already existing on the node.</span><span class="sxs-lookup"><span data-stu-id="3effd-136">Instead, it references the layer already existing on the node.</span></span>

### <a name="manifest"></a><span data-ttu-id="3effd-137">Manifest</span><span class="sxs-lookup"><span data-stu-id="3effd-137">Manifest</span></span>

<span data-ttu-id="3effd-138">Each container image pushed to a container registry is associated with a *manifest*.</span><span class="sxs-lookup"><span data-stu-id="3effd-138">Each container image pushed to a container registry is associated with a *manifest*.</span></span> <span data-ttu-id="3effd-139">The manifest, generated by the registry when the image is pushed, uniquely identifies the image and specifies its layers.</span><span class="sxs-lookup"><span data-stu-id="3effd-139">The manifest, generated by the registry when the image is pushed, uniquely identifies the image and specifies its layers.</span></span> <span data-ttu-id="3effd-140">You can list the manifests for a repository with the Azure CLI command [az acr repository show-manifests][az-acr-repository-show-manifests]:</span><span class="sxs-lookup"><span data-stu-id="3effd-140">You can list the manifests for a repository with the Azure CLI command [az acr repository show-manifests][az-acr-repository-show-manifests]:</span></span>

```azurecli
az acr repository show-manifests --name <acrName> --repository <repositoryName>
```

<span data-ttu-id="3effd-141">For example, listing the manifest digests for the "acr-helloworld" repository:</span><span class="sxs-lookup"><span data-stu-id="3effd-141">For example, listing the manifest digests for the "acr-helloworld" repository:</span></span>

```console
$ az acr repository show-manifests --name myregistry --repository acr-helloworld
[
  {
    "digest": "sha256:0a2e01852872580b2c2fea9380ff8d7b637d3928783c55beb3f21a6e58d5d108",
    "tags": [
      "latest",
      "v3"
    ],
    "timestamp": "2018-07-12T15:52:00.2075864Z"
  },
  {
    "digest": "sha256:3168a21b98836dda7eb7a846b3d735286e09a32b0aa2401773da518e7eba3b57",
    "tags": [
      "v2"
    ],
    "timestamp": "2018-07-12T15:50:53.5372468Z"
  },
  {
    "digest": "sha256:7ca0e0ae50c95155dbb0e380f37d7471e98d2232ed9e31eece9f9fb9078f2728",
    "tags": [
      "v1"
    ],
    "timestamp": "2018-07-11T21:38:35.9170967Z"
  }
]
```

<span data-ttu-id="3effd-142">The manifest discussed here is different from the image manifest you can view in the Azure portal or with [docker manifest inspect][docker-manifest-inspect].</span><span class="sxs-lookup"><span data-stu-id="3effd-142">The manifest discussed here is different from the image manifest you can view in the Azure portal or with [docker manifest inspect][docker-manifest-inspect].</span></span> <span data-ttu-id="3effd-143">In the following section, "manifest digest" refers to the digest generated by the push operation, not the *config.digest* in the image manifest.</span><span class="sxs-lookup"><span data-stu-id="3effd-143">In the following section, "manifest digest" refers to the digest generated by the push operation, not the *config.digest* in the image manifest.</span></span> <span data-ttu-id="3effd-144">You can pull and delete images by **manifest digest**, not config.digest.</span><span class="sxs-lookup"><span data-stu-id="3effd-144">You can pull and delete images by **manifest digest**, not config.digest.</span></span> <span data-ttu-id="3effd-145">The following image illustrates the two types of digests.</span><span class="sxs-lookup"><span data-stu-id="3effd-145">The following image illustrates the two types of digests.</span></span>

![Manifest digest and config.digest in the Azure portal][manifest-digest]

### <a name="manifest-digest"></a><span data-ttu-id="3effd-147">Manifest digest</span><span class="sxs-lookup"><span data-stu-id="3effd-147">Manifest digest</span></span>

<span data-ttu-id="3effd-148">Manifests are identified by a unique SHA-256 hash, or *manifest digest*.</span><span class="sxs-lookup"><span data-stu-id="3effd-148">Manifests are identified by a unique SHA-256 hash, or *manifest digest*.</span></span> <span data-ttu-id="3effd-149">Each image--whether tagged or not--is identified by its digest.</span><span class="sxs-lookup"><span data-stu-id="3effd-149">Each image--whether tagged or not--is identified by its digest.</span></span> <span data-ttu-id="3effd-150">The digest value is unique even if the image's layer data is identical to that of another image.</span><span class="sxs-lookup"><span data-stu-id="3effd-150">The digest value is unique even if the image's layer data is identical to that of another image.</span></span> <span data-ttu-id="3effd-151">This mechanism is what allows you to repeatedly push identically tagged images to a registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-151">This mechanism is what allows you to repeatedly push identically tagged images to a registry.</span></span> <span data-ttu-id="3effd-152">For example, you can repeatedly push `myimage:latest` to your registry without error because each image is identified by its unique digest.</span><span class="sxs-lookup"><span data-stu-id="3effd-152">For example, you can repeatedly push `myimage:latest` to your registry without error because each image is identified by its unique digest.</span></span>

<span data-ttu-id="3effd-153">You can pull an image from a registry by specifying its digest in the pull operation.</span><span class="sxs-lookup"><span data-stu-id="3effd-153">You can pull an image from a registry by specifying its digest in the pull operation.</span></span> <span data-ttu-id="3effd-154">Some systems may be configured to pull by digest because it guarantees the image version being pulled, even if an identically tagged image is subsequently pushed to the registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-154">Some systems may be configured to pull by digest because it guarantees the image version being pulled, even if an identically tagged image is subsequently pushed to the registry.</span></span>

<span data-ttu-id="3effd-155">For example, pulling an image from the "acr-helloworld" repository by manifest digest:</span><span class="sxs-lookup"><span data-stu-id="3effd-155">For example, pulling an image from the "acr-helloworld" repository by manifest digest:</span></span>

```console
$ docker pull myregistry.azurecr.io/acr-helloworld@sha256:0a2e01852872580b2c2fea9380ff8d7b637d3928783c55beb3f21a6e58d5d108
```

> [!IMPORTANT]
> <span data-ttu-id="3effd-156">If you repeatedly push modified images with identical tags, you might create orphaned images--images that are untagged, but still consume space in your registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-156">If you repeatedly push modified images with identical tags, you might create orphaned images--images that are untagged, but still consume space in your registry.</span></span> <span data-ttu-id="3effd-157">Untagged images are not shown in the Azure CLI or in the Azure portal when you list or view images by tag.</span><span class="sxs-lookup"><span data-stu-id="3effd-157">Untagged images are not shown in the Azure CLI or in the Azure portal when you list or view images by tag.</span></span> <span data-ttu-id="3effd-158">However, their layers still exist and consume space in your registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-158">However, their layers still exist and consume space in your registry.</span></span> <span data-ttu-id="3effd-159">The [Delete untagged images](#delete-untagged-images) section of this article discusses freeing space used by untagged images.</span><span class="sxs-lookup"><span data-stu-id="3effd-159">The [Delete untagged images](#delete-untagged-images) section of this article discusses freeing space used by untagged images.</span></span>

## <a name="delete-image-data"></a><span data-ttu-id="3effd-160">Delete image data</span><span class="sxs-lookup"><span data-stu-id="3effd-160">Delete image data</span></span>

<span data-ttu-id="3effd-161">You can delete image data from your container registry in several ways:</span><span class="sxs-lookup"><span data-stu-id="3effd-161">You can delete image data from your container registry in several ways:</span></span>

* <span data-ttu-id="3effd-162">Delete a [repository](#delete-repository): Deletes all images and all unique layers within the repository.</span><span class="sxs-lookup"><span data-stu-id="3effd-162">Delete a [repository](#delete-repository): Deletes all images and all unique layers within the repository.</span></span>
* <span data-ttu-id="3effd-163">Delete by [tag](#delete-by-tag): Deletes an image, the tag, all unique layers referenced by the image, and all other tags associated with the image.</span><span class="sxs-lookup"><span data-stu-id="3effd-163">Delete by [tag](#delete-by-tag): Deletes an image, the tag, all unique layers referenced by the image, and all other tags associated with the image.</span></span>
* <span data-ttu-id="3effd-164">Delete by [manifest digest](#delete-by-manifest-digest): Deletes an image, all unique layers referenced by the image, and all tags associated with the image.</span><span class="sxs-lookup"><span data-stu-id="3effd-164">Delete by [manifest digest](#delete-by-manifest-digest): Deletes an image, all unique layers referenced by the image, and all tags associated with the image.</span></span>

## <a name="delete-repository"></a><span data-ttu-id="3effd-165">Delete repository</span><span class="sxs-lookup"><span data-stu-id="3effd-165">Delete repository</span></span>

<span data-ttu-id="3effd-166">Deleting a repository deletes all of the images in the repository, including all tags, unique layers, and manifests.</span><span class="sxs-lookup"><span data-stu-id="3effd-166">Deleting a repository deletes all of the images in the repository, including all tags, unique layers, and manifests.</span></span> <span data-ttu-id="3effd-167">When you delete a repository, you recover the storage space used by the images that were in that repository.</span><span class="sxs-lookup"><span data-stu-id="3effd-167">When you delete a repository, you recover the storage space used by the images that were in that repository.</span></span>

<span data-ttu-id="3effd-168">The following Azure CLI command deletes the "acr-helloworld" repository and all tags and manifests within the repository.</span><span class="sxs-lookup"><span data-stu-id="3effd-168">The following Azure CLI command deletes the "acr-helloworld" repository and all tags and manifests within the repository.</span></span> <span data-ttu-id="3effd-169">If layers referenced by the deleted manifests are not referenced by any other images in the registry, their layer data is also deleted.</span><span class="sxs-lookup"><span data-stu-id="3effd-169">If layers referenced by the deleted manifests are not referenced by any other images in the registry, their layer data is also deleted.</span></span>

```azurecli
 az acr repository delete --name myregistry --repository acr-helloworld
```

## <a name="delete-by-tag"></a><span data-ttu-id="3effd-170">Delete by tag</span><span class="sxs-lookup"><span data-stu-id="3effd-170">Delete by tag</span></span>

<span data-ttu-id="3effd-171">You can delete individual images from a repository by specifying the repository name and tag in the delete operation.</span><span class="sxs-lookup"><span data-stu-id="3effd-171">You can delete individual images from a repository by specifying the repository name and tag in the delete operation.</span></span> <span data-ttu-id="3effd-172">When you delete by tag, you recover the storage space used by any unique layers in the image (layers not shared by any other images in the registry).</span><span class="sxs-lookup"><span data-stu-id="3effd-172">When you delete by tag, you recover the storage space used by any unique layers in the image (layers not shared by any other images in the registry).</span></span>

<span data-ttu-id="3effd-173">To delete by tag, use [az acr repository delete][az-acr-repository-delete] and specify the image name in the `--image` parameter.</span><span class="sxs-lookup"><span data-stu-id="3effd-173">To delete by tag, use [az acr repository delete][az-acr-repository-delete] and specify the image name in the `--image` parameter.</span></span> <span data-ttu-id="3effd-174">All layers unique to the image, and any other tags associated with the image are deleted.</span><span class="sxs-lookup"><span data-stu-id="3effd-174">All layers unique to the image, and any other tags associated with the image are deleted.</span></span>

<span data-ttu-id="3effd-175">For example, deleting the "acr-helloworld:latest" image from registry "myregistry":</span><span class="sxs-lookup"><span data-stu-id="3effd-175">For example, deleting the "acr-helloworld:latest" image from registry "myregistry":</span></span>

```azurecli
$ az acr repository delete --name myregistry --image acr-helloworld:latest
This operation will delete the manifest 'sha256:0a2e01852872580b2c2fea9380ff8d7b637d3928783c55beb3f21a6e58d5d108' and all the following images: 'acr-helloworld:latest', 'acr-helloworld:v3'.
Are you sure you want to continue? (y/n): y
```

> [!TIP]
> <span data-ttu-id="3effd-176">Deleting *by tag* shouldn't be confused with deleting a tag (untagging).</span><span class="sxs-lookup"><span data-stu-id="3effd-176">Deleting *by tag* shouldn't be confused with deleting a tag (untagging).</span></span> <span data-ttu-id="3effd-177">You can delete a tag with the Azure CLI command [az acr repository untag][az-acr-repository-untag].</span><span class="sxs-lookup"><span data-stu-id="3effd-177">You can delete a tag with the Azure CLI command [az acr repository untag][az-acr-repository-untag].</span></span> <span data-ttu-id="3effd-178">No space is freed when you untag an image because its [manifest](#manifest) and layer data remains in the registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-178">No space is freed when you untag an image because its [manifest](#manifest) and layer data remains in the registry.</span></span> <span data-ttu-id="3effd-179">Only the tag reference itself is deleted.</span><span class="sxs-lookup"><span data-stu-id="3effd-179">Only the tag reference itself is deleted.</span></span>

## <a name="delete-by-manifest-digest"></a><span data-ttu-id="3effd-180">Delete by manifest digest</span><span class="sxs-lookup"><span data-stu-id="3effd-180">Delete by manifest digest</span></span>

<span data-ttu-id="3effd-181">A [manifest digest](#manifest-digest) can be associated with one, none, or multiple tags.</span><span class="sxs-lookup"><span data-stu-id="3effd-181">A [manifest digest](#manifest-digest) can be associated with one, none, or multiple tags.</span></span> <span data-ttu-id="3effd-182">When you delete by digest, all tags referenced by the manifest are deleted, as is layer data for any layers unique to the image.</span><span class="sxs-lookup"><span data-stu-id="3effd-182">When you delete by digest, all tags referenced by the manifest are deleted, as is layer data for any layers unique to the image.</span></span> <span data-ttu-id="3effd-183">Shared layer data is not deleted.</span><span class="sxs-lookup"><span data-stu-id="3effd-183">Shared layer data is not deleted.</span></span>

<span data-ttu-id="3effd-184">To delete by digest, first list the manifest digests for the repository containing the images you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="3effd-184">To delete by digest, first list the manifest digests for the repository containing the images you wish to delete.</span></span> <span data-ttu-id="3effd-185">For example:</span><span class="sxs-lookup"><span data-stu-id="3effd-185">For example:</span></span>

```console
$ az acr repository show-manifests --name myregistry --repository acr-helloworld
[
  {
    "digest": "sha256:0a2e01852872580b2c2fea9380ff8d7b637d3928783c55beb3f21a6e58d5d108",
    "tags": [
      "latest",
      "v3"
    ],
    "timestamp": "2018-07-12T15:52:00.2075864Z"
  },
  {
    "digest": "sha256:3168a21b98836dda7eb7a846b3d735286e09a32b0aa2401773da518e7eba3b57",
    "tags": [
      "v2"
    ],
    "timestamp": "2018-07-12T15:50:53.5372468Z"
  }
]
```

<span data-ttu-id="3effd-186">Next, specify the digest you wish to delete in the [az acr repository delete][az-acr-repository-delete] command.</span><span class="sxs-lookup"><span data-stu-id="3effd-186">Next, specify the digest you wish to delete in the [az acr repository delete][az-acr-repository-delete] command.</span></span> <span data-ttu-id="3effd-187">The format of the command is:</span><span class="sxs-lookup"><span data-stu-id="3effd-187">The format of the command is:</span></span>

```azurecli
az acr repository delete --name <acrName> --image <repositoryName>@<digest>
```

<span data-ttu-id="3effd-188">For example, to delete the last manifest listed in the preceding output (with the tag "v2"):</span><span class="sxs-lookup"><span data-stu-id="3effd-188">For example, to delete the last manifest listed in the preceding output (with the tag "v2"):</span></span>

```console
$ az acr repository delete --name myregistry --image acr-helloworld@sha256:3168a21b98836dda7eb7a846b3d735286e09a32b0aa2401773da518e7eba3b57
This operation will delete the manifest 'sha256:3168a21b98836dda7eb7a846b3d735286e09a32b0aa2401773da518e7eba3b57' and all the following images: 'acr-helloworld:v2'.
Are you sure you want to continue? (y/n): y
```

<span data-ttu-id="3effd-189">The "acr-helloworld:v2" image is deleted from the registry, as is any layer data unique to that image.</span><span class="sxs-lookup"><span data-stu-id="3effd-189">The "acr-helloworld:v2" image is deleted from the registry, as is any layer data unique to that image.</span></span> <span data-ttu-id="3effd-190">If a manifest is associated with multiple tags, all associated tags are also deleted.</span><span class="sxs-lookup"><span data-stu-id="3effd-190">If a manifest is associated with multiple tags, all associated tags are also deleted.</span></span>

## <a name="delete-untagged-images"></a><span data-ttu-id="3effd-191">Delete untagged images</span><span class="sxs-lookup"><span data-stu-id="3effd-191">Delete untagged images</span></span>

<span data-ttu-id="3effd-192">As mentioned in the [Manifest digest](#manifest-digest) section, pushing a modified image using an existing tag **untags** the previously pushed image, resulting in an orphaned (or "dangling") image.</span><span class="sxs-lookup"><span data-stu-id="3effd-192">As mentioned in the [Manifest digest](#manifest-digest) section, pushing a modified image using an existing tag **untags** the previously pushed image, resulting in an orphaned (or "dangling") image.</span></span> <span data-ttu-id="3effd-193">The previously pushed image's manifest--and its layer data--remains in the registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-193">The previously pushed image's manifest--and its layer data--remains in the registry.</span></span> <span data-ttu-id="3effd-194">Consider the following sequence of events:</span><span class="sxs-lookup"><span data-stu-id="3effd-194">Consider the following sequence of events:</span></span>

1. <span data-ttu-id="3effd-195">Push image *acr-helloworld* with tag **latest**: `docker push myregistry.azurecr.io/acr-helloworld:latest`</span><span class="sxs-lookup"><span data-stu-id="3effd-195">Push image *acr-helloworld* with tag **latest**: `docker push myregistry.azurecr.io/acr-helloworld:latest`</span></span>
1. <span data-ttu-id="3effd-196">Check manifests for repository *acr-helloworld*:</span><span class="sxs-lookup"><span data-stu-id="3effd-196">Check manifests for repository *acr-helloworld*:</span></span>

   ```console
   $ az acr repository show-manifests --name myregistry --repository acr-helloworld
   [
     {
       "digest": "sha256:d2bdc0c22d78cde155f53b4092111d7e13fe28ebf87a945f94b19c248000ceec",
       "tags": [
         "latest"
       ],
       "timestamp": "2018-07-11T21:32:21.1400513Z"
     }
   ]
   ```

1. <span data-ttu-id="3effd-197">Modify *acr-helloworld* Dockerfile</span><span class="sxs-lookup"><span data-stu-id="3effd-197">Modify *acr-helloworld* Dockerfile</span></span>
1. <span data-ttu-id="3effd-198">Push image *acr-helloworld* with tag **latest**: `docker push myregistry.azurecr.io/acr-helloworld:latest`</span><span class="sxs-lookup"><span data-stu-id="3effd-198">Push image *acr-helloworld* with tag **latest**: `docker push myregistry.azurecr.io/acr-helloworld:latest`</span></span>
1. <span data-ttu-id="3effd-199">Check manifests for repository *acr-helloworld*:</span><span class="sxs-lookup"><span data-stu-id="3effd-199">Check manifests for repository *acr-helloworld*:</span></span>

   ```console
   $ az acr repository show-manifests --name myregistry --repository acr-helloworld
   [
     {
       "digest": "sha256:7ca0e0ae50c95155dbb0e380f37d7471e98d2232ed9e31eece9f9fb9078f2728",
       "tags": [
         "latest"
       ],
       "timestamp": "2018-07-11T21:38:35.9170967Z"
     },
     {
       "digest": "sha256:d2bdc0c22d78cde155f53b4092111d7e13fe28ebf87a945f94b19c248000ceec",
       "tags": null,
       "timestamp": "2018-07-11T21:32:21.1400513Z"
     }
   ]
   ```

<span data-ttu-id="3effd-200">As you can see in the output of the last step in the sequence, there is now an orphaned manifest whose `"tags"` property is `null`.</span><span class="sxs-lookup"><span data-stu-id="3effd-200">As you can see in the output of the last step in the sequence, there is now an orphaned manifest whose `"tags"` property is `null`.</span></span> <span data-ttu-id="3effd-201">This manifest still exists within the registry, along with any unique layer data that it references.</span><span class="sxs-lookup"><span data-stu-id="3effd-201">This manifest still exists within the registry, along with any unique layer data that it references.</span></span> <span data-ttu-id="3effd-202">**To delete such orphaned images and their layer data, you must delete by manifest digest**.</span><span class="sxs-lookup"><span data-stu-id="3effd-202">**To delete such orphaned images and their layer data, you must delete by manifest digest**.</span></span>

### <a name="list-untagged-images"></a><span data-ttu-id="3effd-203">List untagged images</span><span class="sxs-lookup"><span data-stu-id="3effd-203">List untagged images</span></span>

<span data-ttu-id="3effd-204">You can list all untagged images in your repository using the following Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="3effd-204">You can list all untagged images in your repository using the following Azure CLI command.</span></span> <span data-ttu-id="3effd-205">Replace `<acrName>` and `<repositoryName>` with values appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="3effd-205">Replace `<acrName>` and `<repositoryName>` with values appropriate for your environment.</span></span>

```azurecli
az acr repository show-manifests --name <acrName> --repository <repositoryName>  --query "[?tags==null].digest"
```

### <a name="delete-all-untagged-images"></a><span data-ttu-id="3effd-206">Delete all untagged images</span><span class="sxs-lookup"><span data-stu-id="3effd-206">Delete all untagged images</span></span>

<span data-ttu-id="3effd-207">Use the following sample scripts with caution--deleted image data is UNRECOVERABLE.</span><span class="sxs-lookup"><span data-stu-id="3effd-207">Use the following sample scripts with caution--deleted image data is UNRECOVERABLE.</span></span>

<span data-ttu-id="3effd-208">**Azure CLI in Bash**</span><span class="sxs-lookup"><span data-stu-id="3effd-208">**Azure CLI in Bash**</span></span>

<span data-ttu-id="3effd-209">The following Bash script deletes all untagged images from a repository.</span><span class="sxs-lookup"><span data-stu-id="3effd-209">The following Bash script deletes all untagged images from a repository.</span></span> <span data-ttu-id="3effd-210">It requires the Azure CLI and **xargs**.</span><span class="sxs-lookup"><span data-stu-id="3effd-210">It requires the Azure CLI and **xargs**.</span></span> <span data-ttu-id="3effd-211">By default, the script performs no deletion.</span><span class="sxs-lookup"><span data-stu-id="3effd-211">By default, the script performs no deletion.</span></span> <span data-ttu-id="3effd-212">Change the `ENABLE_DELETE` value to `true` to enable image deletion.</span><span class="sxs-lookup"><span data-stu-id="3effd-212">Change the `ENABLE_DELETE` value to `true` to enable image deletion.</span></span>

> [!WARNING]
> <span data-ttu-id="3effd-213">If you have systems that pull images by manifest digest (as opposed to image name), you should not run this script.</span><span class="sxs-lookup"><span data-stu-id="3effd-213">If you have systems that pull images by manifest digest (as opposed to image name), you should not run this script.</span></span> <span data-ttu-id="3effd-214">Deleting untagged images will prevent those systems from pulling the images from your registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-214">Deleting untagged images will prevent those systems from pulling the images from your registry.</span></span> <span data-ttu-id="3effd-215">Instead of pulling by manifest, consider adopting a *unique tagging* scheme, a [recommended best practice][tagging-best-practices].</span><span class="sxs-lookup"><span data-stu-id="3effd-215">Instead of pulling by manifest, consider adopting a *unique tagging* scheme, a [recommended best practice][tagging-best-practices].</span></span>

```bash
#!/bin/bash

# WARNING! This script deletes data!
# Run only if you do not have systems
# that pull images via manifest digest.

# Change to 'true' to enable image delete
ENABLE_DELETE=false

# Modify for your environment
REGISTRY=myregistry
REPOSITORY=myrepository

# Delete all untagged (orphaned) images
if [ "$ENABLE_DELETE" = true ]
then
    az acr repository show-manifests --name $REGISTRY --repository $REPOSITORY  --query "[?tags==null].digest" -o tsv \
    | xargs -I% az acr repository delete --name $REGISTRY --image $REPOSITORY@% --yes
else
    echo "No data deleted. Set ENABLE_DELETE=true to enable image deletion."
fi
```

<span data-ttu-id="3effd-216">**Azure CLI in PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3effd-216">**Azure CLI in PowerShell**</span></span>

<span data-ttu-id="3effd-217">The following PowerShell script deletes all untagged images from a repository.</span><span class="sxs-lookup"><span data-stu-id="3effd-217">The following PowerShell script deletes all untagged images from a repository.</span></span> <span data-ttu-id="3effd-218">It requires PowerShell and the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3effd-218">It requires PowerShell and the Azure CLI.</span></span> <span data-ttu-id="3effd-219">By default, the script performs no deletion.</span><span class="sxs-lookup"><span data-stu-id="3effd-219">By default, the script performs no deletion.</span></span> <span data-ttu-id="3effd-220">Change the `$enableDelete` value to `$TRUE` to enable image deletion.</span><span class="sxs-lookup"><span data-stu-id="3effd-220">Change the `$enableDelete` value to `$TRUE` to enable image deletion.</span></span>

> [!WARNING]
> <span data-ttu-id="3effd-221">If you have systems that pull images by manifest digest (as opposed to image name), you should not run this script.</span><span class="sxs-lookup"><span data-stu-id="3effd-221">If you have systems that pull images by manifest digest (as opposed to image name), you should not run this script.</span></span> <span data-ttu-id="3effd-222">Deleting untagged images will prevent those systems from pulling the images from your registry.</span><span class="sxs-lookup"><span data-stu-id="3effd-222">Deleting untagged images will prevent those systems from pulling the images from your registry.</span></span> <span data-ttu-id="3effd-223">Instead of pulling by manifest, consider adopting a *unique tagging* scheme, a [recommended best practice][tagging-best-practices].</span><span class="sxs-lookup"><span data-stu-id="3effd-223">Instead of pulling by manifest, consider adopting a *unique tagging* scheme, a [recommended best practice][tagging-best-practices].</span></span>

```powershell
# WARNING! This script deletes data!
# Run only if you do not have systems
# that pull images via manifest digest.

# Change to '$TRUE' to enable image delete
$enableDelete = $FALSE

# Modify for your environment
$registry = "myregistry"
$repository = "myrepository"

if ($enableDelete) {
    az acr repository show-manifests --name $registry --repository $repository --query "[?tags==null].digest" -o tsv `
    | %{ az acr repository delete --name $registry --image $repository@$_ --yes }
} else {
    Write-Host "No data deleted. Set `$enableDelete = `$TRUE to enable image deletion."
}
```

## <a name="next-steps"></a><span data-ttu-id="3effd-224">Next steps</span><span class="sxs-lookup"><span data-stu-id="3effd-224">Next steps</span></span>

<span data-ttu-id="3effd-225">For more information about image storage in Azure Container Registry see [Container image storage in Azure Container Registry](container-registry-storage.md).</span><span class="sxs-lookup"><span data-stu-id="3effd-225">For more information about image storage in Azure Container Registry see [Container image storage in Azure Container Registry](container-registry-storage.md).</span></span>

<!-- IMAGES -->
[manifest-digest]: ./media/container-registry-delete/01-manifest-digest.png

<!-- LINKS - External -->
[docker-manifest-inspect]: https://docs.docker.com/edge/engine/reference/commandline/manifest/#manifest-inspect
[portal]: https://portal.azure.com
[tagging-best-practices]: https://blogs.msdn.microsoft.com/stevelasker/2018/03/01/docker-tagging-best-practices-for-tagging-and-versioning-docker-images/

<!-- LINKS - Internal -->
[az-acr-repository-delete]: /cli/azure/acr/repository#az-acr-repository-delete
[az-acr-repository-show-manifests]: /cli/azure/acr/repository#az-acr-repository-show-manifests
[az-acr-repository-untag]: /cli/azure/acr/repository#az-acr-repository-untag
