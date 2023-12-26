# libspice 
The Simple Protocol for Independent Computing Environments

SPICE is a remote desktop protocol used most often for viewing virtual machine consoles. It is used by QEMU to provide high-performance graphical interfaces to running VMs.

This is an optional dependency of the QEMU KCP package. Other optional dependencies are usbredir, libslirp, and libvirglrenderer. You can install all of them like this:

```
kcp -u
kcp -i libspice
kcp -i usbredir
kcp -i libslirp
kcp -i libvirglrenderer
```
