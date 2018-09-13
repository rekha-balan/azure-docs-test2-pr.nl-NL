---
title: Azure FileUpload UI element | Microsoft Docs
description: Describes the Microsoft.Common.FileUpload UI element for Azure portal.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/05/2018
ms.author: tomfitz
ms.openlocfilehash: 2886dbafe6bf20718f4e3cd2976764fc432dbb04
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867834"
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="fbe99-103">Microsoft.Common.FileUpload UI element</span><span class="sxs-lookup"><span data-stu-id="fbe99-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="fbe99-104">A control that allows a user to specify one or more files to upload.</span><span class="sxs-lookup"><span data-stu-id="fbe99-104">A control that allows a user to specify one or more files to upload.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fbe99-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="fbe99-105">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="fbe99-107">Schema</span><span class="sxs-lookup"><span data-stu-id="fbe99-107">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="fbe99-108">Remarks</span><span class="sxs-lookup"><span data-stu-id="fbe99-108">Remarks</span></span>
- <span data-ttu-id="fbe99-109">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span><span class="sxs-lookup"><span data-stu-id="fbe99-109">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="fbe99-110">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span><span class="sxs-lookup"><span data-stu-id="fbe99-110">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="fbe99-111">The default value is **null**.</span><span class="sxs-lookup"><span data-stu-id="fbe99-111">The default value is **null**.</span></span>
- <span data-ttu-id="fbe99-112">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span><span class="sxs-lookup"><span data-stu-id="fbe99-112">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="fbe99-113">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="fbe99-113">The default value is **false**.</span></span>
- <span data-ttu-id="fbe99-114">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="fbe99-114">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="fbe99-115">If **file** is specified, the output has the contents of the file as a blob.</span><span class="sxs-lookup"><span data-stu-id="fbe99-115">If **file** is specified, the output has the contents of the file as a blob.</span></span> <span data-ttu-id="fbe99-116">If **url** is specified, then the file is uploaded to a temporary location, and the output has the URL of the blob.</span><span class="sxs-lookup"><span data-stu-id="fbe99-116">If **url** is specified, then the file is uploaded to a temporary location, and the output has the URL of the blob.</span></span> <span data-ttu-id="fbe99-117">Temporary blobs will be purged after 24 hours.</span><span class="sxs-lookup"><span data-stu-id="fbe99-117">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="fbe99-118">The default value is **file**.</span><span class="sxs-lookup"><span data-stu-id="fbe99-118">The default value is **file**.</span></span>
- <span data-ttu-id="fbe99-119">An uploaded file is protected.</span><span class="sxs-lookup"><span data-stu-id="fbe99-119">An uploaded file is protected.</span></span> <span data-ttu-id="fbe99-120">The output URL includes a [SAS token](../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for accessing the file during deployment.</span><span class="sxs-lookup"><span data-stu-id="fbe99-120">The output URL includes a [SAS token](../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for accessing the file during deployment.</span></span>
- <span data-ttu-id="fbe99-121">The value of `options.openMode` determines how the file is read.</span><span class="sxs-lookup"><span data-stu-id="fbe99-121">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="fbe99-122">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span><span class="sxs-lookup"><span data-stu-id="fbe99-122">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="fbe99-123">The default value is **text**.</span><span class="sxs-lookup"><span data-stu-id="fbe99-123">The default value is **text**.</span></span>
- <span data-ttu-id="fbe99-124">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span><span class="sxs-lookup"><span data-stu-id="fbe99-124">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="fbe99-125">`options.encoding` specifies the encoding to use when reading the file.</span><span class="sxs-lookup"><span data-stu-id="fbe99-125">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="fbe99-126">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span><span class="sxs-lookup"><span data-stu-id="fbe99-126">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fbe99-127">Sample output</span><span class="sxs-lookup"><span data-stu-id="fbe99-127">Sample output</span></span>
<span data-ttu-id="fbe99-128">If options.multiple is false and options.uploadMode is file, then the output has the contents of the file as a JSON string:</span><span class="sxs-lookup"><span data-stu-id="fbe99-128">If options.multiple is false and options.uploadMode is file, then the output has the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="fbe99-129">If options.multiple is true and\`options.uploadMode is file, then the output has the contents of the files as a JSON array:</span><span class="sxs-lookup"><span data-stu-id="fbe99-129">If options.multiple is true and\`options.uploadMode is file, then the output has the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="fbe99-130">If options.multiple is false and options.uploadMode is url, then the output has a URL as a JSON string:</span><span class="sxs-lookup"><span data-stu-id="fbe99-130">If options.multiple is false and options.uploadMode is url, then the output has a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="fbe99-131">If options.multiple is true and options.uploadMode is url, then the output has a list of URLs as a JSON array:</span><span class="sxs-lookup"><span data-stu-id="fbe99-131">If options.multiple is true and options.uploadMode is url, then the output has a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="fbe99-132">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span><span class="sxs-lookup"><span data-stu-id="fbe99-132">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="fbe99-133">You may need to right-click individual links to copy the full URLs.</span><span class="sxs-lookup"><span data-stu-id="fbe99-133">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fbe99-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbe99-134">Next steps</span></span>
* <span data-ttu-id="fbe99-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbe99-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="fbe99-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fbe99-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
