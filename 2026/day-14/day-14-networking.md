# Day 13 – Linux Volume Management (LVM)

Today I learned how **Linux Logical Volume Management (LVM)** works and how it allows flexible disk management.
With LVM, storage can be **created, resized, and extended dynamically** without needing to repartition disks.

---

# Step 0 – Switch to Root User

```bash
sudo -i
```

This allows running LVM commands without permission issues.

---

# Step 1 – Create Virtual Disk (If No Spare Disk)

Create a 1GB virtual disk file:

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
```

Attach it as a loop device:

```bash
losetup -fP /tmp/disk1.img
```

Check loop devices:

```bash
losetup -a
```

Example Output:

```
/dev/loop0: [2065]:123456 (/tmp/disk1.img)
```

---

# Task 1 – Check Current Storage

Commands used:

```bash
lsblk
pvs
vgs
lvs
df -h
```

Example Output:

```
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
loop0    7:0    0 1G  0 loop
```

Observation:

* No physical volumes or volume groups exist yet.

---

# Task 2 – Create Physical Volume

Create a physical volume:

```bash
pvcreate /dev/loop0
```

Verify:

```bash
pvs
```

Example Output:

```
PV         VG        Fmt  Attr PSize PFree
/dev/loop0           lvm2 ---  1.00g 1.00g
```

---

# Task 3 – Create Volume Group

Create a volume group named **devops-vg**:

```bash
vgcreate devops-vg /dev/loop0
```

Verify:

```bash
vgs
```

Example Output:

```
VG        #PV #LV #SN Attr   VSize  VFree
devops-vg   1   0   0 wz--n- 1.00g 1.00g
```

---

# Task 4 – Create Logical Volume

Create a **500MB logical volume**:

```bash
lvcreate -L 500M -n app-data devops-vg
```

Verify:

```bash
lvs
```

Example Output:

```
LV       VG        Attr       LSize
app-data devops-vg -wi-a----- 500.00m
```

---

# Task 5 – Format and Mount Logical Volume

Format the logical volume:

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

Create mount directory:

```bash
mkdir -p /mnt/app-data
```

Mount the volume:

```bash
mount /dev/devops-vg/app-data /mnt/app-data
```

Verify mount:

```bash
df -h /mnt/app-data
```

Example Output:

```
Filesystem                     Size  Used Avail Use% Mounted on
/dev/mapper/devops--vg-app--data 492M  24K  455M   1% /mnt/app-data
```

---

# Task 6 – Extend the Volume

Extend the logical volume by **200MB**:

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

Resize filesystem:

```bash
resize2fs /dev/devops-vg/app-data
```

Verify new size:

```bash
df -h /mnt/app-data
```

Example Output:

```
Filesystem                     Size  Used Avail Use% Mounted on
/dev/mapper/devops--vg-app--data 688M  24K  640M   1% /mnt/app-data
```

---

# Commands Used

```
sudo -i
dd
losetup
lsblk
pvcreate
pvs
vgcreate
vgs
lvcreate
lvs
mkfs.ext4
mkdir
mount
df -h
lvextend
resize2fs
```

---

# What I Learned

1. **LVM provides flexible storage management** by separating physical storage from logical volumes.
2. Storage can be **extended without downtime** by resizing logical volumes.
3. LVM structure consists of:

```
Physical Volume (PV) → Volume Group (VG) → Logical Volume (LV)
```

---

# Why LVM Matters in DevOps

LVM is useful in real-world environments because:

* Storage can be extended dynamically as applications grow.
* It allows better disk management for servers and databases.
* It is commonly used in **cloud servers, Kubernetes nodes, and enterprise Linux systems**.

---

# Screenshots Included

```
lsblk-output.png
pvcreate-output.png
vgcreate-output.png
lvcreate-output.png
lvextend-output.png
```

---

# LinkedIn Post

**Day 13 of #90DaysOfDevOps**

Today I learned Linux Logical Volume Management (LVM).

I created physical volumes, volume groups, and logical volumes, then extended storage dynamically without repartitioning the disk.

This is a powerful feature used in production servers.

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
