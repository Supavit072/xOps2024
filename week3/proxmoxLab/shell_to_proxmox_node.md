## Ubuntu Cloud Images
- wget https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64-disk-kvm.img
- wget http://rustdesk.ipv9.me/iso/jammy-server-cloudimg-amd64.img
## Set Up
- qm create 8000 --core 2 --memory 2048 --name u2204CloudTemplate --net0 virtio,bridge=vmbr0 --serial0 socket --agent enabled=1
- qm importdisk 8000 jammy-server-cloudimg-amd64.img diskpool
- qm set 8000 --scsihw virtio-scsi-pci --scsi0 diskpool:vm-8000-disk-0
- qm resize 8000 scsi0 +8G
- qm set 8000 --ide2 diskpool:cloudinit
- qm set 8000 --boot c --bootdisk scsi0
