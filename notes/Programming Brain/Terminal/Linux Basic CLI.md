# Linux Basic CLI

The command line is a tool or interface for interacting with a computer using only text rather than the mouse.

Command-line is an essential tool for software development. We can execute a wide variety of programs on our computer through this. In this tutorial, we are going to learn the necessary UNIX commands for development.

**UNIX** command is a type of command that is used in LINUX and macOS.

### Check the Current Directory

On the command line, it's important to know the directory we are currently working on. For that, we can use `pwd` command.

```bash
pwd
```

### Display List of Files

To see the list of files and directories in the current directory use `ls` command in your CLI.

```bash
ls
```

Shows all of my files and directories of my Current directory.

- To show the contents of a directory pass the directory name to the `ls` command i.e. `ls directory_name`.
- Some useful `ls` command options:-

| Option | Description |
| --- | --- |
| `ls -a` | list all files including hidden file starting with '.’ |
| `ls -l` | list with the long format |
| `ls -la` | list long format including hidden files |

### Create a Directory

We can create a new folder using the `mkdir` command. To use it type `mkdir folder_name`.

```bash
mkdir new folder
```

Use `ls` command to see the directory is created or not.

### Move Between Directories

It's used to change directory or to move other directories. To use it type `cd directory_name`.

```bash
cd project
```

Can use `pwd` command to confirm your directory name.

### Parent Directory

We have seen `cd` command to change directory but if we want to move back or want to move to the parent directory we can use a special symbol `..` after `cd` command, like `cd ..`

```bash
cd ..
```

### Create Files

We can create an empty file by typing `touch file_name`. It's going to create a new file in the current directory (the directory you are currently in) with your provided name.

```bash
touch hello.txt
```

I created a `hello.txt` file in my current working directory. Again you can use `ls` command to see the file is created or not.

Now open your **hello.txt** file in your text editor and write ***Hello Everyone!*** into your **hello.txt** file and save it.

Now open your `hello.txt` file in your text editor and write `Hello Everyone!` into your `hello.txt` file and save it.

### Display the Content of a File

We can display the content of a file using the `cat` command. To use it type `cat file_name`.

```bash
cat hello.txt
```

Shows the content of my `hello.txt` file.

### Move Files & Directories

To move a file and directory, we use `mv` command.
By typing `mv file_to_move destination_directory`, you can move a file to the specified directory.

By entering `mv directory_to_move destination_directory`, you can move all the files and directories under that directory.

```bash
mv hello.txt project
```

### Rename Files & Directories

`mv` command can also be used to rename a file and a directory.

You can rename a file by typing `mv old_file_name new_file_name` & also rename a directory by typing `mv old_directory_name new_directory_name`.

```bash
mv hello.txt hi.txt
```

Renamed my `hello.txt` file to the `hi.txt` file.

### Copy Files & Directories

To do this, we use the `cp` command.
• You can copy a file by entering `cp file_to_copy new_file_name`.

```bash
cp hi.txt hello.txt
```

Copied my `hi.txt` file content into `hello.txt` file. For confirmation open your `hello.txt` file in your text editor.

• You can also copy a directory by adding the `-r` option, like `cp -r directory_to_copy new_directory_name`.

The `-r` option for "recursive" means that it will copy all of the files including the files inside of subfolders.

### Remove Files & Directories

To do this, we use the `rm` command.
• To remove a file, you can use the command like `rm file_to_remove`.

```bash
rm hi.txt
```

Here I removed my `hi.txt` file.

• To remove a directory, use the command like `rm -r directory_to_remove`.

```bash
rm -r folder
```

I removed my `folder` directory from my `project` directory i.e. current working directory.

### Clear Screen

Clear command is used to clear the terminal screen.

```bash
clear
```

### Home Directory

The Home directory is represented by `~`. The Home directory refers to the base directory for the user. If we want to move to the Home directory we can use `cd ~` command. Or we can only use `cd` command.

```bash
cd ~
```

### Linux Path

**PATH** is an environmental variable in Linux and other Unix-like operating systems that tells the shell which directories to search for executable files (i.e., ready-to-run programs) in response to commands issued by a user.

There are two basic types of paths:

1. **Absolute path:** It is also known as full path. It is the location of a filesystem object relative to the root directory.
2. **Relative Path:** Relative paths are relative to the present working directory. A list of special relative paths is listed in the table below.

| Relative Path | Description | Example | Notes |
| --- | --- | --- | --- |
| `.` | Present working directory | `ls .` | List contents of the current directory |
| `..` | Parent directory | `cd ..` | Go one level up to the parent directory |
| `-` | Previous working directory | `cd -` | Go back to the previous working directory |

### Linux Flags

Linux commands can be tuned to our requirements by providing flags along with the command when calling them. These are usually a hyphen (-) followed by an alphabet eg: -a, -B etc or double-hyphen (--) followed by text eg: --all, --color

**Flags** are a way to set options and pass in arguments to the commands you run. Commands you run will change their behavior based on what flags are set.

But, how will we find a flag for our purpose?

Commands come with a "Manual" as well. We can access it using the `man` command followed by the name of the command we need to see the manual of. For `ls`, we do `man ls` and you will get this-.

- **NAME** - name of the command & short description of what it does
- **SYNPOSIS** - how the command is used
- **DESCRIPTION** - detailed info on the usage of the command

### Linux filesystems

A Linux file system is a structured collection of files on a disk drive or a partition. A partition is a segment of memory and contains some specific data. In our machine, there can be various partitions of the memory. Generally, every partition contains a file system.

The Linux file system contains the following sections:

- The entire Linux directory structure starting at the top (/) root directory.
- A specific data storage format (EXT3, EXT4, BTRFS, XFS and so on)
- A partition or logical volume having a particular file system.

The final building block is the software required to implement all of these functions. Linux uses a two-part software implementation as a way to improve both system and programmer efficiency.

[https___dev-to-uploads.s3.amazonaws.com_i_3lng7pe475d2iq9r4cgt.avif](Linux%20Basic%20CLI%201b2aeacbb29981009ccbefb34572d75c/https___dev-to-uploads.s3.amazonaws.com_i_3lng7pe475d2iq9r4cgt.avif)

### Linux Directory Structure

[https___dev-to-uploads.s3.amazonaws.com_i_uhc3hiyfli6efyf9es74.avif](Linux%20Basic%20CLI%201b2aeacbb29981009ccbefb34572d75c/https___dev-to-uploads.s3.amazonaws.com_i_uhc3hiyfli6efyf9es74.avif)

Let's understand the naming conventions.

![https___dev-to-uploads.s3.amazonaws.com_i_9pq7kvzj7ftxs3b2o53x.png](Linux%20Basic%20CLI%201b2aeacbb29981009ccbefb34572d75c/https___dev-to-uploads.s3.amazonaws.com_i_9pq7kvzj7ftxs3b2o53x.png)