# ci20
files for CI20 (MIPS Creator CI20 V2)

This u-boot is created to boot off from sd-card drive.
version of this u-boot is ci20-v2013.10
In order to boot from this device, you need to switch jumper JP3 from 1-2 to 2-3 on ci20.
To prepare drive you need to do such operation on sd-card:

sudo sfdisk /dev/sdx -L << EOF

2M,,L

EOF

x is letter of your device, you check that by using lsblk

sudo mkfs.ext4 /dev/sdx1

dd if=/dev/zero of=/dev/sdx bs=1K seek=526 count=32

sudo dd if=u-boot-spl.bin of=/dev/sdx obs=512 seek=1

dd if=u-boot.img of=/dev/sdx obs=1K seek=14

sync
