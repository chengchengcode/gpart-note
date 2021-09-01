# gpart-note
Add a new 8T disk to ubuntu with gpart.

1, find the disk name:

>sudo fdisk -l

...
Disk /dev/sdb: 7.3 TiB, 8001563222016 bytes, 15628053168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 4096 bytes / 33553920 bytes
...

So the /dev/sdb is the disk I need.

2, use parted to make th patition:

>sudo parted /dev/sdb

Make label:

>mklabel gpt

Format all the disk

>mkpart primary 0 -1

>print
>quit

3, Check and format

>lsblk 

Then format it:

>sudo mkfs.ext4 -F /dev/sdb1

Now the disk is ready. The user of this disk is root, so I

4, change the owner:

>cd /media/cheng/
>ls -al

drwxr-xr-x  8 cheng root 4096 8月  10 09:37 2c11f2a4-d08c-44eb-93b8-70a1658ced81
drwxr-xr-x  3 root  root 4096 9月   1 13:45 fb49ce8d-832a-49d7-a402-aacef6dd4560

>sudo chown cheng fb49ce8d-832a-49d7-a402-aacef6dd4560

Now the disk is installed in /media/cheng/fb49ce8d-832a-49d7-a402-aacef6dd4560

