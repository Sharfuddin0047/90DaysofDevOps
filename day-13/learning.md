# 📅 Day 13 – Linux Volume Management (LVM)

## 🎯 Objective

Understand and practice LVM:

* Create Physical Volume (PV)
* Create Volume Group (VG)
* Create Logical Volume (LV)
* Format & Mount
* Extend Logical Volume

---

# 🔐 Step 0 – Switch to Root

```bash
sudo -i
```

---

# 🧱 Step 1 – Check Current Storage

```bash
lsblk
pvs
vgs
lvs
df -h
```

## 📝 Observation:

* `lsblk` shows disks and partitions.
* `pvs` shows physical volumes.
* `vgs` shows volume groups.
* `lvs` shows logical volumes.
* `df -h` shows mounted filesystem usage.

---

# 💽 Step 2 – Create Virtual Disk (If No Extra Disk)

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
losetup -fP /tmp/disk1.img
losetup -a
```

---

# 🧩 Step 3 – Create Physical Volume (PV)

```bash
pvcreate /dev/loop0
pvs
```

## 📝 Learned:

* PV initializes disk for LVM use.

---

# 🏗 Step 4 – Create Volume Group (VG)

```bash
vgcreate devops-vg /dev/loop0
vgs
```

## 📝 Learned:

* VG combines one or more physical volumes.
* Acts like a storage pool.

---

# 📦 Step 5 – Create Logical Volume (LV)

```bash
lvcreate -L 500M -n app-data devops-vg
lvs
```

## 📝 Learned:

* LV is like a flexible partition.
* Size can be extended later.

---

# 🗂 Step 6 – Format and Mount

```bash
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```

## 📝 Learned:

* Filesystem required before mount.
* After mounting, usable like normal directory.

---

# 📈 Step 7 – Extend the Volume

```bash
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```

## 📝 Learned:

* `lvextend` increases LV size.
* `resize2fs` resizes filesystem.
* No need to unmount in most cases.

---

# 🧠 Key Concepts Summary

LVM Structure:

```
Disk → PV → VG → LV → Filesystem → Mount
```

* PV = Physical disk
* VG = Storage pool
* LV = Flexible partition

---

# 🚀 What I Learned (3 Points)

1. LVM allows dynamic resizing without downtime.
2. Storage can be extended easily in production.
3. Logical volumes are more flexible than traditional partitions.

---

# 🧹 (Optional) Cleanup Commands

If you want to remove everything:

```bash
umount /mnt/app-data
lvremove /dev/devops-vg/app-data
vgremove devops-vg
pvremove /dev/loop0
losetup -d /dev/loop0
rm -f /tmp/disk1.img
```

