# Links

## Hard Links

A hard link is a direct connection between a file's name and the physical data on the hard drive. Instead of making a duplicate, a hard link gives the data a new name. Both the initial file and the new hard link point to the exact same location on the disk.

+ You can access the data from the hard link even if the first file is deleted.
+ There is no "original" file. All ordinary files are hard links.
+ Hard links don't use extra space, no matter how many links you make.
+ Hard links can only link regular files. You cannot use them on directories.
+ Hard links must be on the same filesystem. They cannot cross different drives or partitions.
+ Changes to one of the hard links will reflect on all the others, since they all point to the same data on disk.


**How to create a hard link**:
```
# Create a file
echo "Hello World" > file1.txt

# Create a hard link called 'file2.txt' pointing to the same data as 'file1.txt'.
ln file1.txt file2.txt

cat file2.txt
# Output: Hello World
```

### Check Hard Links Count For A File

**Using `ls`:**
```
ls -l myfile
```

Sample output:
```
-rw-r--r-- 3 raymond raymond 1024 Jul 17 10:30 myfile
```

The `3` after the permissions is the hard link count. It means 3 files in total point to that data on disk.

**Using `stat`:**
```
stat myfile
```

Sample Output:
```
File: myfile
Size: 1024
Links: 3
```

The `Links:` field is the hard link count.

### Find All Hard Links To The File

1. Get the inode number:
  ```
  ls -i myfile
  ```

  Sample Output:
  ```
  1234567 myfile
  ```
2. Search for that inode:
  ```
  find /path/to/search -xdev -inum 1234567
  ```

  The `-xdev` option limits the search to the same filesystem, since hard links cannot span filesystems.

---
