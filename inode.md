# Inode
---

## References
---
- [ ] [Inode in Operating System - geeksforgeeks](https://www.geeksforgeeks.org/inode-in-operating-system/)
- [ ] [What does an Inode Contain? - geeksforgeeks](https://practice.geeksforgeeks.org/problems/what-does-an-inode-contain)
- [ ] [Linux inodes Explained](https://www.youtube.com/watch?v=6KjMlm8hhFA)
- [ ] [Linux Essentials - Symbolic Links](https://www.youtube.com/watch?v=zfSa-PEU3h4)
- [ ] [Hard and Soft Links in Linux](https://www.youtube.com/watch?v=kYonC93SvpE)

## Introduction
---
In Unix based operating system each file is indexed by an Inode. Inode are special disk blocks they are created when the file system is created. The number of Inode limits the total number of files/directories that can be stored in the file system. 

The Inode contains the following information: 
```
14 Bytes            	2 Bytes
File name 1	i-node 1
File name 2	i-node 2
Directory name 1	i-node 3
```
## Inode Content
---
- Mode/permission (protection)
- Owner ID
- Group ID
- Size of file
- Number of hard links to the file
- Time last accessed
- Time last modified
- Time inode last modified
- File protection flags
- Pointers to the blocks storing file’s contents
---
- Administrative information (permissions, timestamps, etc).
- A number of direct blocks (typically 12) that contains to the first 12 blocks of the files.
- A single indirect pointer that points to a disk block which in turn is used as an index block, if the file is too big to be indexed entirely by the direct blocks.
- A double indirect pointer that points to a disk block which is a collection of pointers to disk blocks which are index blocks, used if the file is too big to beindexed by the direct and single indirect blocks.
- A triple indirect pointer that points to an index block of index blocks of index blocks.

### `NAME` of the file is not present in the inode
---
The reason for separating out file name from the other information related to same file is for maintaining hard-links to files. This means that once all the other information is separated out from the file name then we can have various file names which point to same inode.

## Inode Total Size
---
- Number of disk block address possible to store in 1 disk block = (Disk Block Size / Disk Block Address).
- Small files need only the direct blocks, so there is little waste in space or extra disk reads in those cases. Medium sized files may use indirect blocks. Only large files make use of the double or triple indirect blocks, and that is reasonable since those files are large anyway.The disk is now broken into two different types of blocks: Inode and Data Blocks.
- There must be some way to determine where the Inodes are, and to keep track of free Inodes and disk blocks. This is done by a Superblock. Superblock is located at a fixed position in the file system. The Superblock is usually replicated on the disk to avoid catastrophic failure in case of corruption of the main Superblock.
- Index allocation schemes suffer from some of the same performance problems. As does linked allocation. For example, the index blocks an be cached in memory, but the data blocks may be spread all over a partition.

## Basic Setup
---
```bash
cat > ~/Documents/lang.txt <<EOF
python
golang
JavaScript
Java
C
C++
EOF
```
```bash
mkdir Documents/src/
```
to see inode of a file, use -i flag
```bash
ls -lai Documents/
```
```
total 16
664326 drwxr-xr-x  3 raktim raktim 4096 Jan 31 17:57 .
405893 drwxr-xr-x 24 raktim raktim 4096 Jan 31 15:44 ..
660141 -rw-rw-r--  1 raktim raktim   36 Jan 31 15:49 lang.txt
659944 drwxrwxr-x  2 raktim raktim 4096 Jan 31 17:57 src
```

## Human readable format
---
```bash
ls -laih Documents/
```
```
total 16K
664326 drwxr-xr-x  3 raktim raktim 4.0K Jan 31 17:57 .
405893 drwxr-xr-x 23 raktim raktim 4.0K Jan 31 18:04 ..
660141 -rw-rw-r--  1 raktim raktim   36 Jan 31 15:49 lang.txt
659944 drwxrwxr-x  2 raktim raktim 4.0K Jan 31 17:57 src
```
inode permission symlink_count owner group size(?) last_mod_date file_name

`total 16`

reference : `man 1 ls`
```
In addition, for each directory whose contents are
displayed, the total number of 512-byte blocks used by the files in the directory is
displayed on a line by itself, immediately before the information for the files in
the directory.
```
here `. = Documents/`, and it has 3 symlinks.

reason being, there are 3 instances - 
- `Documents/`
- `.`  - within `Documents/`
- `..` - within `src/`

```bash
stat Documents/lang.txt
```
```
  File: Documents/lang.txt
  Size: 36        	Blocks: 8          IO Block: 4096   regular file
Device: fd00h/64768d	Inode: 660141      Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1001/  raktim)   Gid: ( 1001/  raktim)
Access: 2022-01-31 15:49:41.175501681 +0000
Modify: 2022-01-31 15:49:32.847339344 +0000
Change: 2022-01-31 15:49:32.847339344 +0000
 Birth: -
```
