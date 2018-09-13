The NC and NV sizes are also known as GPU-enabled instances. These are specialized virtual machines that include NVIDIA's GPU cards, optimized for different scenarios and use cases. The NV sizes are optimized and designed for remote visualization, streaming, gaming, encoding and VDI scenarios utilizing frameworks such as OpenGL and DirectX. The NC sizes are more optimized for compute-intensive and network-intensive applications and algorithms, including CUDA- and OpenCL-based applications and simulations. 


The NV instances are powered by NVIDIA’s Tesla M60 GPU card and NVIDIA GRID for desktop accelerated applications and virtual desktops where customers will be able to visualize their data or simulations. Users will be able to visualize their graphics intensive workflows on the NV instances to get superior graphics capability and additionally run single precision workloads such as encoding and rendering. The Tesla M60 delivers 4096 CUDA cores in a dual-GPU design with up to 36 streams of 1080p H.264. 

The NC instances are powered by NVIDIA’s Tesla K80 card. Users can now crunch through data much faster by leveraging CUDA for energy exploration applications, crash simulations, ray traced rendering, deep learning and more. The Tesla K80 delivers 4992 CUDA cores with a dual-GPU design, up to 2.91 Teraflops of double-precision and up to 8.93 Teraflops of single-precision performance.

## <a name="nv-instances"></a>NV instances

| Size | CPU cores | Memory: GiB | Local SSD: GiB | GPU |
| --- | --- | --- | --- | --- |
| Standard_NV6 |6 |56 |380 | 1 |
| Standard_NV12 |12 |112 |680 | 2 |
| Standard_NV24 |24 |224 |1440 | 4 |

1 GPU = one-half M60 card.

**Supported operating systems**

* Windows Server 2016, Windows Server 2012 R2 - see [N-series driver setup for Windows](../articles/virtual-machines/windows/n-series-driver-setup.md)

## <a name="nc-instances"></a>NC instances

| Size | CPU cores | Memory: GiB | Local SSD: GiB | GPU |
| --- | --- | --- | --- | --- |
| Standard_NC6 |6 |56 | 380 | 1 |
| Standard_NC12 |12 |112 | 680 | 2 |
| Standard_NC24 |24 |224 | 1440 | 4 |
| Standard_NC24r* |24 |224 | 1440 | 4 |

1 GPU = one-half K80 card.

*RDMA capable

**Supported operating systems**

* Windows Server 2016, Windows Server 2012 R2 - see [N-series driver setup for Windows](../articles/virtual-machines/windows/n-series-driver-setup.md)
* Ubuntu 16.04 LTS - see [N-series driver setup for Linux](../articles/virtual-machines/linux/n-series-driver-setup.md)

<br>

