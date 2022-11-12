# myvms
Bhyve Virtual Manager configuration


    pkg install vm-bhyve grub2-bhyve bhyve-firmware qemu-tools tmux
    
    vi /boot/loader.conf
    vmm_load="YES"
	nmdm_load="YES"
	bridge_load="YES"
	tap_load="YES"

	vi /etc/sysctl.conf
    net.link.tap.up_on_open=1
    net.inet.ip.forwarding=1
    
    zfs create trinity/virtuals
    zfs set mountpoint=/vms trinity/virtuals
    zfs set recordsize=64K trinity/virtuals
    
    sysrc vm_enable="YES"
    sysrc vm_dir="zfs:trinity/virtuals"
    vm init
    cp /usr/local/share/examples/vm-bhyve/* /vms/.templates/ 
    vm switch create virtuals
    vm switch add virtuals em0
    vm iso /usr/home/samob/Documents/FreeBSD/FreeBSD-13.1-RELEASE-amd64-bootonly.iso
    
    vi /vms/.templates/freebsd-zvol.conf # edit bridge directive to match "virtuals"
    
    vm create -t freebsd-zvol -s 120G 13template
    vm install 13template FreeBSD-13.1-RELEASE-amd64-bootonly.iso
    vm console 13template


