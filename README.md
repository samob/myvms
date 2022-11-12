# myvms
Bhyve Virtual Manager configuration

1. pkg install vm-bhyve grub2-bhyve bhyve-firmware qemu-tools
2. zfs create neo/virtuals && zfs set mountpoint=/vms neo/virtuals (zfs set recordsize=64K neo/virtuals)
3. sysrc vm_enable="YES"
4. sysrc vm_dir="zfs:neo/virtuals"
5. vm init
6. cp /usr/local/share/examples/vm-bhyve/* /vms/.templates/ # edit bridge to myvirtuals
7. vm switch create myvirtuals
8. vm switch add myvirtuals re0
9. vm iso https://download.freebsd.org/ftp/releases/ISO-IMAGES/13.1/FreeBSD-13.1-RELEASE-amd64-bootonly.iso
10. vm create mybsd
11. vm install [-f] mybsd FreeBSD-11.2-RELEASE-amd64-bootonly.iso
12. vm console mybsd

