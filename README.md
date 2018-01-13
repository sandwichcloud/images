# images
Official Images to use on Sandwich Cloud

All images are built using packer with a qcow2 output, converted to vmdk then
packed into a tarball with gzip compression.

Install Requirements:

```
yum install epel-release
yum install qemu-system-x86 qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client virt-install virt-viewer
```

Usage:

```
export IMAGE_DIR="centos/7"
export IMAGE_NAME=`echo $IMAGE_DIR | tr / -`
packer build -var "image_dir=$IMAGE_DIR" -var "image_name=$IMAGE_NAME" $IMAGE_DIR/packer.json
qemu-img convert -f qcow2 -O vmdk output/$IMAGE_NAME output/$IMAGE_NAME.vmdk
tar -cvzf output/$IMAGE_NAME.tar.gz -C output/ $IMAGE_NAME.vmdk
```
