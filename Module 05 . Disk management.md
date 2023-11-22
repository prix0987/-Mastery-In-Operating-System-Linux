## What is Disk Partition In Linux 

Disk Partitioning is the process of dividing a disk into one or more logical areas, often known as partitions, on which the user can work separately. It is one step of disk formatting. If a partition is created, the disk will store the information about the location and size of partitions in the partition table. With the partition table, each partition can appear to the operating system as a logical disk, and users can read and write data on those disks. The main advantage of disk partitioning is that each partition can be managed separately.

### Create Partitions in the Disk
Power on the system and log in to the system. Ensure that you are logged in as root (or any user of the sudo group). Once the system UI comes up, open the Terminal.  To view the available Hard Disks in our system, use the command lsblk or cat /proc/partitions. Both commands will display the same results, but in different ways. 

```bash
  lsblk
```

![Logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141556/GeeksForGeeks10.jpg)

We can find that the system has two disks -> sda and sdb. sda is our older Hard Disk. We can say so, as that disk is already partitioned as sda1 and sda2. We can partition the disk using CLI as well as GUI. We will demonstrate CLI based partitioning in this article.

```bash
  fdisk -l 
```

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141729/GeeksForGeeks14.jpg)

We found that the Hard Disk that we are going to partition can be found at /dev/sdb. Use the command.

```bash
  fdisk /dev/sdb
```

It will take us to a different console where we can use the partitioning specific commands. We will be concentrating more on the following commands (or flags).

```bash
m  -> help
p  -> print partition table
n  -> create new partition
d  -> delete partition
q  -> quit without writing
w  -> write to disk
```

While partitioning, we should be aware of certain factors. 

On a disk, we can have a maximum of four partitions.
The partitions are of two types.
- Primary
- Extended
- Extended partitions can have logical partitions inside it.
- Among the four possible partitions, the possible combinations are.
- All 4 primary partitions
- 3 primary partitions and 1 extended partition

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141752/GeeksForGeeks15.jpg)


```bash
n
```
This will create a new partition. Specify the type of partition using the p for primary and e for extended.



```bash
p
```

This will create a primary partition. The console will prompt for the number to be given to the partition. We can give any number from 1 to 4. Let me give 1. Then choose the starting position (cylinder) of partition 1. Press enters to start partitioning from the beginning of the disk. 

You can specify the size of the partition in two ways, either as the last cylinder number or by specifying the size directly. If we need partition1 to be of 4 GB size (as a whole number), use.

```bash
+4G 
```
Pressing enter will create our 1st partition successfully. Follow the same steps, until we create 4 partitions on our newly attached disk. 

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141808/GeeksForGeeks16.jpg)
create our 1st partition successfully

We have created 3 primary partitions and an extended partition in the disk. The extended partition, as the name suggests, can be further divided into multiple logical partitions. Once 4 partitions are created, no more partitions can be created on the same disk. We can check whether we have done the partitioning in the right way by printing the partition table using the p command. If everything is as per the expectation, then write the changes to the disk using the w command, else use the q command to quit without writing. 

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141824/GeeksForGeeks17.jpg)

### Create a File System on the Partition

Computers use particular kinds of file systems to store and organize data on media, like Hard Disk, CD, DVD, etc. The commonly used Linux file systems are ext2, ext3, ext4, JFS, ReiserFS, XFS, FAT (usually in Windows OS) and B-treeFS. Inorder to specify the file system to be used in each partition, we can use the mkfs (make file system) command.

```bash
mkfs.ext4 -j /dev/sdb1
```

What this command does is that it will make the first partition’s file system to be ext4 (format the partition to ext4). -j flag is used to allow/support journaling. It helps in throwing errors into the journal, in case of system failure.

```bash
mkfs.fat /dev/sdb2
```

This command is used to format the 2nd partition available in /dev/sdb2 to the FAT file system. Even though we formatted the disks, it is of no use to us, unless we mount it on a directory.

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141919/GeeksForGeeks20.jpg)

### Mounting the file systems 

Let us make three directories, for mounting the first, second, and third partition using the mkdir (make directory) command.

```bash
mkdir /mount1
mkdir /mount2
mkdir /mount3
```
Mounting the formatted partitions can be achieved using the mount command.

```bash
mount /dev/sdb1 /mount1
mount /dev/sdb2 /mount2
mount /dev/sdb3 /mount3
```

The first part of the command is the keyword mount, followed by the partition and the directory to which the mounting is to be done. To view the disk details, we can use the df command. h flag helps to display the output in a human-readable format.

```bash
df -h
```

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141924/GeeksForGeeks23.jpg)

Unmounting a disk can be achieved by unmount command.

```bash
unmount /dev/sdb2
```

All these mountains are temporary in nature. Once we reboot the system, mounting will be reverted. To make it permanent, we must edit the File System Table of the Operating System. We should be highly careful whirling with this file. A small error in this file can cause the system to be unbootable and can make the entire system to be useless. Let us open the file in any editor (I will be using the VI editor).


```bash
vi /etc/fstab
```

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141925/GeeksForGeeks24.jpg)

Add our mounted file systems’ details in the file, in the order.

```bash
mounted partition        [ space ]         directory      [ space ]           file system type          [ space ]          defaults         [ space ]         0            [ space ]             0 
```

Save the file and come back to the terminal. Mount the partitions permanently using the mount -a command 

```bash
mount -a
```
![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141927/GeeksForGeeks25.jpg)

We can verify whether our partitions are available for our purposes by visiting the root folder of the Operating System (since we have mounted the partitions on the mount1, mount2, mount3 directories in the root folder). We can also verify the existence of our newly created partitions using the lsblk command. 

```bash
lsblk
```

We can find our partitions in the table, each of 4 GB size.

![logo](https://media.geeksforgeeks.org/wp-content/uploads/20210112141929/GeeksForGeeks27.jpg)

