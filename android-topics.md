
# VNDK (Vendor Native Development Kit)
https://source.android.com/devices/architecture/vndk?hl=en

VNDK is a set of shared libraries for vendors to implement vendor modules.
○ Part of VINTF
○ Versioned, stable
## Concepts:
* __Same-process HAL (SP-HAL)__
* __Dynamic linker & Dynamic Linker Namespace__
* 


# VINTF (Vendor Interface Object)
https://source.android.com/devices/architecture/vintf




TREBLE

# AAOS Virtualization
Cuttlefish
TROUT

## gRPC

https://chromium.googlesource.com/chromiumos/platform2/+/6c976ef165ee22ddf274035d16b8e2071b29cb0f/vm_tools/README.md
https://chromium.googlesource.com/chromiumos/platform2/+/6c976ef165ee22ddf274035d16b8e2071b29cb0f/vm_tools/docs/vsock.md
https://www.gitmemory.com/issue/kata-containers/kata-containers/1327/768476008
https://github.com/grpc/grpc/issues/25801
https://grpc.github.io/grpc/core/md_doc_core_transport_explainer.html
https://vrushaliraut1234.medium.com/grpc-concepts-with-example-b37a028470dd
https://grpc.io/docs/platforms/android/java/quickstart/
https://static.sched.com/hosted_files/devconfcz2020a/b1/DevConf.CZ_2020_vsock_v1.1.pdf
https://android.googlesource.com/device/google/trout/+/refs/heads/master/hal/vehicle/2.0/GrpcVehicleClient.cpp
https://medium.com/swlh/a-beginners-guide-to-grpc-in-android-61cc56a423f7

### Crosscompile grpc for QNX
https://github.com/grpc/grpc/issues/16918
https://stackoverflow.com/questions/62385485/not-able-to-cross-compile-grpc-for-qnx-platform-using-aarch64-unknown-nto-qnx7-0

Google had changed https://cs.android.com/android/platform/superproject/+/master:external/grpc-grpc/src/core/ext/filters/client_channel/parse_address.cc;l=77?q=AF_VSOCK&sq=&ss=android%2Fplatform%2Fsuperproject:external%2Fgrpc-grpc%2F
to add VSOCK support.
