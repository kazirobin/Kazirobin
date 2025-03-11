# FS Module

Node.js file system: To handle file operations like creating, reading, deleting, etc., Node.js provides an inbuilt module called FS (File System). Node.js gives the functionality of file I/O by providing wrappers around the standard POSIX functions. All file system operations can have synchronous and asynchronous forms depending upon user requirements. To use this File System module, use the require() method:

```jsx
const fs = require('fs');
```

## Common use for File System module:

- Read Files
- Write Files
- Append Files
- Close Files
- Delete Files

## What is Synchronous and Asynchronous approach?

- **Synchronous approach:** They are called **blocking functions** as it waits for each operation to complete, only after that, it executes the next operation, hence blocking the next command from execution i.e. a command will not be executed until & unless the query has finished executing to get all the result from previous commands.
- **Asynchronous approach:** They are called **non-blocking functions** as it never waits for each operation to complete, rather it executes all operations in the first go itself. The result of each operation will be handled once the result is available i.e. each command will be executed soon after the execution of the previous command. While the previous command runs in the background and loads the result once it is finished processing the data.

## Reading a File

Use the `fs.readFile()` method to read the physical file asynchronously.

```jsx
fs.readFile(fileName [,options], callback)
```

### Parameter Description:

- filename: Full path and name of the file as a string.
- options: The options parameter can be an object or string which can include encoding and flag. The default encoding is utf8 and default flag is `"r"`.
- callback: A function with two parameters `err` and `data`. This will get called when `readFile` operation completes.

The following example demonstrates reading existing `TestFile.txt` asynchronously.

```jsx
const fs = require('fs');

fs.readFile('TestFile.txt', function (err, data) {
    if (err) 
        throw err;

    console.log(data.toString());
});
```

The above example reads `TestFile.txt` (on Windows) asynchronously and executes callback function when read operation completes. This read operation either throws an error or completes successfully. The err parameter contains error information if any. The data parameter contains the content of the specified file.

Use the `fs.readFileSync()` method to read file synchronously, as shown below.

```jsx
const fs = require('fs');

const data = fs.readFileSync('dummyfile.txt', 'utf8');
console.log(data.toString());
```

## Writing a File

Use the `fs.writeFile()` method to write data to a file. If file already exists then it overwrites the existing content otherwise it creates a new file and writes data into it.

```jsx
fs.writeFile(filename, data[, options], callback)
```

### Parameter Description:

- filename: Full path and name of the file as a string.
- Data: The content to be written in a file.
- options: The options parameter can be an object or string which can include encoding, mode and flag. The default encoding is utf8 and default flag is `"r"`.
- callback: A function with two parameters err and fd. This will get called when write operation completes.

The following example creates a new file called test.txt and writes "Hello World" into it asynchronously.

```jsx
const fs = require("fs");

fs.writeFile("test.txt", "Hello World!", function (err) {
  if (err) {
    console.log(err);
  } else {
    console.log("Write operation complete.");
  }
});
```

In the same way, use the `fs.appendFile()` method to append the content to an existing file.

```jsx
const fs = require("fs");

fs.appendFile("test.txt", "Hello World!", function (err) {
  if (err) {
    console.log(err);
  } else {
    console.log("Append operation complete.");
  }
});
```

## Open File

Alternatively, you can open a file for reading or writing using the `fs.open()` method.

```jsx
fs.open(path, flags[, mode], callback)
```

### Parameter Description:

- path: Full path with name of the file as a string.
- Flag: The flag to perform operation
- Mode: The mode for read, write or readwrite. Defaults to 0666 readwrite.
- callback: A function with two parameters `err` and `data`. This will get called when file open operation completes.

## Flags

The following table lists all the flags which can be used in read/write operation.

| Flag | Description |
| --- | --- |
| r | Open file for reading. An exception occurs if the file does not exist. |
| r+ | Open file for reading and writing. An exception occurs if the file does not exist. |
| rs | Open file for reading in synchronous mode. |
| rs+ | Open file for reading and writing, telling the OS to open it synchronously. See notes for 'rs' about using this with caution. |
| w | Open file for writing. The file is created (if it does not exist) or truncated (if it exists). |
| wx | Like 'w' but fails if path exists. |
| w+ | Open file for reading and writing. The file is created (if it does not exist) or truncated (if it exists). |
| wx+ | Like 'w+' but fails if path exists. |
| a | Open file for appending. The file is created if it does not exist. |
| ax | Like 'a' but fails if path exists. |
| a+ | Open file for reading and appending. The file is created if it does not exist. |
| ax+ | Like 'a+' but fails if path exists. |

## Delete File

Use the `fs.unlink()` method to delete an existing file.

```jsx
fs.unlink(path, callback);
```

The following example deletes an existing file.

```jsx
const fs = require("fs");

fs.unlink("test.txt", function () {
  console.log("File Deleted Successfully.");
});
```

## Important method of fs module

| Method | Description |
| --- | --- |
| fs.readFile(fileName [,options], callback) | Reads existing file. |
| fs.writeFile(filename, data[, options], callback) | Writes to the file. If file exists then overwrite the content otherwise creates new file. |
| fs.open(path, flags[, mode], callback) | Opens file for reading or writing. |
| fs.rename(oldPath, newPath, callback) | Renames an existing file. |
| fs.chown(path, uid, gid, callback) | Asynchronous chown. |
| fs.stat(path, callback) | Returns fs.stat object which includes important file statistics. |
| fs.link(srcpath, dstpath, callback) | Links file asynchronously. |
| fs.unlink(path, callback); | Delete a file. |
| fs.symlink(destination, path[, type], callback) | Symlink asynchronously. |
| fs.rmdir(path, callback) | Renames an existing directory. |
| fs.mkdir(path[, mode], callback) | Creates a new directory. |
| fs.readdir(path, callback) | Reads the content of the specified directory. |
| fs.utimes(path, atime, mtime, callback) | Changes the timestamp of the file. |
| fs.exists(path, callback) | Determines whether the specified file exists or not. |
| fs.access(path[, mode], callback) | Tests a user's permissions for the specified file. |
| fs.appendFile(file, data[, options], callback) | Appends new content to the existing file. |

[Directory Method](FS%20Module%201b2aeacbb299812db920d39353177ab5/Directory%20Method%201b2aeacbb29981368d04e872d4de614f.md)