# Essential Linux Commands for DevOps

This document provides an overview of the most commonly used Linux commands in DevOps. Knowing how to implement these commands in the Linux terminal is crucial before advancing to other tools and technologies.

---

## **Basic Commands**

1. **pwd** - Print working directory.  
   Example: `pwd` (Displays the current directory path)

2. **ls** - List directory contents.  
   Example: `ls -l` (Lists files in long format)

3. **cd** - Change directory.  
   Example: `cd /home/user` (Changes to the `/home/user` directory)

4. **mkdir** - Make directories.  
   Example: `mkdir mydir` (Creates a directory named `mydir`)

5. **rmdir** - Remove empty directories.  
   Example: `rmdir mydir` (Removes the directory named `mydir`)

6. **rm** - Remove files or directories.  
   Example: `rm -r mydir` (Removes directory `mydir` and its contents)

7. **cp** - Copy files or directories.  
   Example: `cp file1 file2` (Copies `file1` to `file2`)

8. **mv** - Move/rename files or directories.  
   Example: `mv file1 newfile1` (Renames `file1` to `newfile1`)

9. **touch** - Create an empty file or update the timestamp of a file.  
   Example: `touch newfile` (Creates an empty file named `newfile`)

10. **cat** - Concatenate and display file content.  
    Example: `cat file1` (Displays the content of `file1`)

11. **echo** - Display a line of text.  
    Example: `echo "Hello, World!"` (Prints "Hello, World!" to the terminal)

12. **less** - View file content one screen at a time.  
    Example: `less file1` (Views the content of `file1` page by page)

13. **more** - View file content one screen at a time.  
    Example: `more file1` (Displays the content of `file1` page by page)

14. **head** - Output the first part of a file.  
    Example: `head -n 5 file1` (Displays the first 5 lines of `file1`)

15. **tail** - Output the last part of a file.  
    Example: `tail -n 5 file1` (Displays the last 5 lines of `file1`)

...

---

## **Intermediate Commands**

31. **scp** - Secure copy (remote file copy program).  
    Example: `scp file1 user@remote:/path` (Copies `file1` to a remote server)

32. **ssh** - OpenSSH client (remote login program).  
    Example: `ssh user@remote-server.com` (Connects to the remote server via SSH)

33. **rsync** - Remote file and directory synchronization.  
    Example: `rsync -av /src /dest` (Synchronizes `/src` to `/dest`)

34. **tar** - Archive files.  
    Example: `tar -cvf myarchive.tar mydir` (Creates a tar archive of `mydir`)

35. **gzip** - Compress files.  
    Example: `gzip file1` (Compresses `file1`)

...

---

## **Advanced Commands**

61. **awk** - Pattern scanning and processing language.  
    Example: `awk '{print $1}' file1` (Prints the first column of `file1`)

62. **sed** - Stream editor for filtering and transforming text.  
    Example: `sed 's/hello/hi/g' file1` (Replaces all occurrences of "hello" with "hi" in `file1`)

63. **xargs** - Build and execute command lines from standard input.  
    Example: `echo file1 file2 | xargs rm` (Removes `file1` and `file2`)

64. **cut** - Remove sections from each line of files.  
    Example: `cut -d':' -f1 /etc/passwd` (Displays the first field from `/etc/passwd`)

65. **sort** - Sort lines of text files.  
    Example: `sort file1` (Sorts the lines in `file1`)

...

---

Feel free to explore each command by using `man <command>` to view the manual and understand all possible options. These commands form a strong foundation in Linux, which is essential in the field of DevOps.

You can View More commands by downloading the raw linux cheat sheet 

THANK YOU
---
