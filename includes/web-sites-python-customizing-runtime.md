<span data-ttu-id="6657d-101">Azure will determine the version of Python to use for its virtual environment with the following priority:</span><span class="sxs-lookup"><span data-stu-id="6657d-101">Azure will determine the version of Python to use for its virtual environment with the following priority:</span></span>

1. <span data-ttu-id="6657d-102">version specified in runtime.txt in the root folder</span><span class="sxs-lookup"><span data-stu-id="6657d-102">version specified in runtime.txt in the root folder</span></span>
2. <span data-ttu-id="6657d-103">version specified by Python setting in the web app configuration (the **Settings** > **Application Settings** blade for your web app in the Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="6657d-103">version specified by Python setting in the web app configuration (the **Settings** > **Application Settings** blade for your web app in the Azure Portal)</span></span>
3. <span data-ttu-id="6657d-104">python-2.7 is the default if none of the above are specified</span><span class="sxs-lookup"><span data-stu-id="6657d-104">python-2.7 is the default if none of the above are specified</span></span>

<span data-ttu-id="6657d-105">Valid values for the contents of</span><span class="sxs-lookup"><span data-stu-id="6657d-105">Valid values for the contents of</span></span> 

    \runtime.txt

<span data-ttu-id="6657d-106">are:</span><span class="sxs-lookup"><span data-stu-id="6657d-106">are:</span></span>

* <span data-ttu-id="6657d-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="6657d-107">python-2.7</span></span>
* <span data-ttu-id="6657d-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="6657d-108">python-3.4</span></span>

<span data-ttu-id="6657d-109">If the micro version (third digit) is specified, it is ignored.</span><span class="sxs-lookup"><span data-stu-id="6657d-109">If the micro version (third digit) is specified, it is ignored.</span></span>

