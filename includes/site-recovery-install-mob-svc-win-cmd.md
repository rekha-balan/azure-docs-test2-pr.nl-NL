1. <span data-ttu-id="416f9-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span><span class="sxs-lookup"><span data-stu-id="416f9-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span></span> <span data-ttu-id="416f9-102">Run the following commands as an administrator at a command prompt:</span><span class="sxs-lookup"><span data-stu-id="416f9-102">Run the following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="416f9-103">To install Mobility Service, run the following command:</span><span class="sxs-lookup"><span data-stu-id="416f9-103">To install Mobility Service, run the following command:</span></span>

  ```
  UnifiedAgent.exe /Role "Agent" /CSEndpoint "IP address of the configuration server" /PassphraseFilePath <Full path to the passphrase file>``
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="416f9-104">Mobility Service installer command-line arguments</span><span class="sxs-lookup"><span data-stu-id="416f9-104">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation directory>] [/CSIP <IP address>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log file path>]<br/>
```

  | <span data-ttu-id="416f9-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="416f9-105">Parameter</span></span>|<span data-ttu-id="416f9-106">Type</span><span class="sxs-lookup"><span data-stu-id="416f9-106">Type</span></span>|<span data-ttu-id="416f9-107">Description</span><span class="sxs-lookup"><span data-stu-id="416f9-107">Description</span></span>|<span data-ttu-id="416f9-108">Possible values</span><span class="sxs-lookup"><span data-stu-id="416f9-108">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="416f9-109">/Role</span><span class="sxs-lookup"><span data-stu-id="416f9-109">/Role</span></span>|<span data-ttu-id="416f9-110">Mandatory</span><span class="sxs-lookup"><span data-stu-id="416f9-110">Mandatory</span></span>|<span data-ttu-id="416f9-111">Specifies whether Mobility Service should be installed</span><span class="sxs-lookup"><span data-stu-id="416f9-111">Specifies whether Mobility Service should be installed</span></span>|<span data-ttu-id="416f9-112">Agent</span><span class="sxs-lookup"><span data-stu-id="416f9-112">Agent</span></span> </br> <span data-ttu-id="416f9-113">MasterTarget</span><span class="sxs-lookup"><span data-stu-id="416f9-113">MasterTarget</span></span>|
  |<span data-ttu-id="416f9-114">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="416f9-114">/InstallLocation</span></span>|<span data-ttu-id="416f9-115">Mandatory</span><span class="sxs-lookup"><span data-stu-id="416f9-115">Mandatory</span></span>|<span data-ttu-id="416f9-116">Location where Mobility Service is installed</span><span class="sxs-lookup"><span data-stu-id="416f9-116">Location where Mobility Service is installed</span></span>|<span data-ttu-id="416f9-117">Any folder on the computer</span><span class="sxs-lookup"><span data-stu-id="416f9-117">Any folder on the computer</span></span>|
  |<span data-ttu-id="416f9-118">/CSIP</span><span class="sxs-lookup"><span data-stu-id="416f9-118">/CSIP</span></span>|<span data-ttu-id="416f9-119">Mandatory</span><span class="sxs-lookup"><span data-stu-id="416f9-119">Mandatory</span></span>|<span data-ttu-id="416f9-120">IP address of the configuration server</span><span class="sxs-lookup"><span data-stu-id="416f9-120">IP address of the configuration server</span></span>| <span data-ttu-id="416f9-121">Any valid IP address</span><span class="sxs-lookup"><span data-stu-id="416f9-121">Any valid IP address</span></span>|
  |<span data-ttu-id="416f9-122">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="416f9-122">/PassphraseFilePath</span></span>|<span data-ttu-id="416f9-123">Mandatory</span><span class="sxs-lookup"><span data-stu-id="416f9-123">Mandatory</span></span>|<span data-ttu-id="416f9-124">Location of the passphrase</span><span class="sxs-lookup"><span data-stu-id="416f9-124">Location of the passphrase</span></span> |<span data-ttu-id="416f9-125">Any valid UNC or local file path</span><span class="sxs-lookup"><span data-stu-id="416f9-125">Any valid UNC or local file path</span></span>|
  |<span data-ttu-id="416f9-126">/LogFilePath</span><span class="sxs-lookup"><span data-stu-id="416f9-126">/LogFilePath</span></span>|<span data-ttu-id="416f9-127">Optional</span><span class="sxs-lookup"><span data-stu-id="416f9-127">Optional</span></span>|<span data-ttu-id="416f9-128">Location of the installation log</span><span class="sxs-lookup"><span data-stu-id="416f9-128">Location of the installation log</span></span>|<span data-ttu-id="416f9-129">Any valid folder on the computer</span><span class="sxs-lookup"><span data-stu-id="416f9-129">Any valid folder on the computer</span></span>|

#### <a name="example"></a><span data-ttu-id="416f9-130">Example</span><span class="sxs-lookup"><span data-stu-id="416f9-130">Example</span></span>

```
  UnifiedAgent.exe /Role "Agent" /CSEndpoint "I192.168.2.35" /PassphraseFilePath "C:\Temp\MobSvc.passphrase"
```
