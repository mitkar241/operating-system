# inode
---
#### basic setup
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
#### Human readable format
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

#### total 16
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
## References
---
- [ ] [Linux inodes Explained](https://www.youtube.com/watch?v=6KjMlm8hhFA)
- [ ] [Linux Essentials - Symbolic Links](https://www.youtube.com/watch?v=zfSa-PEU3h4)
- [ ] [Hard and Soft Links in Linux](https://www.youtube.com/watch?v=kYonC93SvpE)
