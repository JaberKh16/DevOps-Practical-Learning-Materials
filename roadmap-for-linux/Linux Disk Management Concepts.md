# Linux Disk Management – Deep Concepts and Commands

## 1. Overview

Linux disk management involves understanding block devices, partitions, file systems, and volume-management layers. Core activities include inspecting devices, partitioning disks, formatting, mounting, resizing, and monitoring disk I/O performance.

---

## 2. Block Devices

### List Block Devices

`lsblk -fa`

Key flags:

- `-f` → show file systems
    
- `-a` → include empty devices
    

### Detailed Device Info

`blkid`

`udevadm info --query=all --name=/dev/sda`

---

## 3. Partition Tables

Linux uses:

- **MBR (msdos)** – Legacy, supports up to 2 TB, 4 primary partitions.
    
- **GPT** – Modern, supports large disks, unlimited partitions, checksums.
    

### View Partition Table

`sudo fdisk -l sudo parted -l`

---

## 4. Partitioning Disks

### Using `fdisk` (MBR/GPT interactive tool)

**Warning:** Modifying partitions can erase data.  
Example:

`sudo fdisk /dev/sda`

Inside:

- `n` → new partition
    
- `d` → delete
    
- `t` → type
    
- `w` → write changes
    

### Using `parted` (Gives more precision)

`sudo parted /dev/sdb (parted) mklabel gpt (parted) mkpart primary ext4 1MiB 100%`

### Using `sfdisk` (Scriptable, advanced)

Dump table:

`sudo sfdisk -d /dev/sda > sda.backup`

Restore:

`sudo sfdisk /dev/sda < sda.backup`

---

## 5. File Systems

### Create File Systems

**Ext4**

`sudo mkfs.ext4 /dev/sdb1`

**XFS**

`sudo mkfs.xfs /dev/sdb1`

**F2FS (flash storage)**

`sudo mkfs.f2fs /dev/sdb1`

### Check File System

`sudo fsck -f /dev/sdb1`

---

## 6. Mounting and Unmounting

### Mount

`sudo mount /dev/sdb1 /mnt`

### Unmount

`sudo umount /mnt`

### Mount options example

`sudo mount -o noatime,defaults /dev/sdc2 /mnt/data`

---

## 7. `/etc/fstab` – Persistent Mounts

Edit:

`sudo nano /etc/fstab`

Example entry:

`UUID=xxxx-xxxx   /mnt/data   ext4   defaults,noatime   0 2`

View UUID:

`blkid`

Test `fstab` without reboot:

`sudo mount -a`

---

## 8. LVM (Logical Volume Manager)

LVM enables flexible resizing, snapshots, and multi-disk volumes.

### Core components:

- **PV** (Physical Volume) – device layer
    
- **VG** (Volume Group) – storage pool
    
- **LV** (Logical Volume) – usable disk volumes
    

### Create PV

`sudo pvcreate /dev/sdb1`

### Create VG

`sudo vgcreate myvg /dev/sdb1`

### Create LV

`sudo lvcreate -L 20G -n mylv myvg`

### Format LV

`sudo mkfs.ext4 /dev/myvg/mylv`

### Resize LV (extend)

`sudo lvextend -L +10G /dev/myvg/mylv sudo resize2fs /dev/myvg/mylv   # For ext4`

---

## 9. Disk Usage Analysis

### Basic

`df -h`

`du -sh /path/*`

### Find largest directories

`du -h --max-depth=1 / | sort -hr | head`

---

## 10. Disk I/O Monitoring

### Real-time I/O

`iostat -xz 1`

### Monitor I/O ops per process

`iotop`

### Low-level statistics

`cat /proc/diskstats`

---

## 11. SMART Disk Health

Install:

`sudo apt install smartmontools`

Check health:

`sudo smartctl -H /dev/sda`

Full report:

`sudo smartctl -a /dev/sda`

Self-test:

`sudo smartctl -t long /dev/sda`

---

## 12. Disk Cloning and Imaging

### Clone entire disk (dangerous)

`sudo dd if=/dev/sda of=/dev/sdb bs=64K conv=noerror,sync status=progress`

### Create image

`sudo dd if=/dev/sda of=disk.img status=progress`

---

## 13. RAID (mdadm)

### Create RAID 1 example

`sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc`

Check status:

`cat /proc/mdstat`

Stop RAID:

`sudo mdadm --stop /dev/md0`

---

## 14. Filesystem Resize Without LVM

### Ext4 (grow)

`sudo resize2fs /dev/sdb1`

### XFS (grow only)

`sudo xfs_growfs /mount/point`

### Shrinking ext4 (requires unmounted)

`sudo umount /dev/sdb1 sudo resize2fs /dev/sdb1 20G`

---

## 15. Wiping Disks

### Wipe partition table

`sudo wipefs -a /dev/sdb`

### Overwrite disk

`sudo dd if=/dev/zero of=/dev/sdb status=progress`

---

If you want, I can also prepare:

- A version with diagrams
    
- A version specifically for NVMe
    
- A cheatsheet version
    
- A full 40-page advanced `.md` document with workflow examples
    

Tell me what depth you want.