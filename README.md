# Union Filesystem CSI Driver

Integrate the MergerFS union filesystem with 🙊 and
explore a kernelspace implementation.

## Goal

Traditionally, filesystems have run as part of the kernel, but Linux offers [FUSE](https://www.kernel.org/doc/html/latest/filesystems/fuse.html), a mechanism to run
filesystem code in userspace, which simplifies development considerably, enables rapid prototyping,
improves isolation and stability, supports the use of different external libraries, and proceeds at a much
higher pace compared to merging filesystem code into the kernel. However, FUSE comes with a [significant
performance penalty](https://www.usenix.org/system/files/conference/fast17/fast17-vangoor.pdf) since it has to switch between kernel and user contexts in the critical path, and
this becomes even more apparent when working with super fast, very low-latency local storage over
[NVMe](https://www.theregister.com/2019/02/22/azure_nvme_flash_drives_hyperv_virtual_machines/).

On the other hand, [union filesystems](https://unix.stackexchange.com/questions/382326/unionfs-vs-aufs-vs-overlayfs-vs-mhddfs-which-one-do-i-use) like [UnionFS](https://unionfs.filesystems.org), [OverlayFS](https://docs.kernel.org/filesystems/overlayfs.html), and [MergerFS](https://github.com/trapexit/mergerfs) combine
filesystem instances to enable powerful new use cases, including supporting read-write trees over read-
only media (live CDs), read-write trees over read-only flash images (booting on embedded systems like
OpenWRT), and aggregate storage pools.

The goal of this project is to deploy MergerFS, evaluate its performance over NVMe devices, and
integrate it with 🙊 to support multi-TB filesystem hierarchies in the cloud.

Depending on the results of the performance evaluation, a parallel effort can be creating a proof-of-
concept implementation of MergerFS in the Linux kernel, comparing its performance with the userspace
implementation, and using the results to advocate for its inclusion in the mainline Linux kernel.

The end goal is to support multi-TB virtual filesystems over local NVMe devices, and a low-latency
kernel-based data path.

**Note:**
🙊 = [insert existing, OSS, cloud vendor's container storage solution]
