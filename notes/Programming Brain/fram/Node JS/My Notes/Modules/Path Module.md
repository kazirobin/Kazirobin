# Path Module

`CreatedAt - 07 May 2024` `RevisedAt -`  

The path module in Node.js is a built-in module that provides utilities for working with file and directory paths. It helps in constructing, manipulating, and working with file and directory paths in a cross-platform manner, making it easier to write platform-independent code.

All we need to do is require and include it in our file.

```jsx
const path = require('path');
```

Let’s get information out of a path with those methods.

`basename`: get the filename part
`dirname`: get the parent folder of a file
`extname`: get the file extension

```jsx
const path = require('path');

/*Example*/
const image = 'C:/user/foo/image.png';
console.log(path.basename(image)); // image.png
console.log(path.dirname(image)); // C:/user/foo 
console.log(path.extname(image)); // .png
```

## path.basename(path, [ext]):

Returns the last portion of a path (i.e., the filename). You can also specify an extension to remove.

```jsx
const path = require('path');

const filename = path.basename('/path/to/file.txt'); // Returns 'file.txt'
```

## path.dirname(path):

Returns the directory name of a path.

```jsx
const path = require('path');

const dirname = path.dirname('/path/to/file.txt'); // Returns '/path/to'
```

## path.extname(path):

Returns the file extension of a path, including the dot.

```jsx
const path = require('path');

const extension = path.extname('/path/to/file.txt'); // Returns '.txt'
```

## path.normalize(path):

Normalizes a path by resolving '..' and '.' segments and removing redundant slashes.

```jsx
const path = require('path');

const normalizedPath = path.normalize('/path/to/../file.txt'); // Returns '/path/file.txt'
```

## path.join([...paths]):

Joins one or more path segments into a single path, using the appropriate platform-specific separator (e.g., "\" on Windows and "/" on Unix-like systems).

Let’s assume we have a path called `mainpath`. We would like to create a folder called `testfolder` and in the folder we will have a file called `image.png`. We can use the `path.join()` method to concatenate these three parts of a path to create a platform independent path.

```jsx
const path = require('path');

const mainpath = "C:Desktop/user/foo/sample.txt";
const image = "image.png";
console.log(path.join(path.dirname(mainpath), "testfolder", image));
```

The output is as shown below for windows machines.

`C:Desktop\user\foo\testfolder\image.png`

## path.resolve([...paths]):

Resolves an absolute path from relative paths. It returns an absolute path by combining the current working directory with the provided paths.

```jsx
const path = require('path');

const absolutePath = path.resolve('folder', 'file.txt');
```

## path.isAbsolute(path):

Check if a path is an absolute path.

```jsx
const path = require('path');

const isAbsolute = path.isAbsolute('/path/to/file.txt'); // Returns true
```

These are just a few of the functions provided by the path module. The module is particularly useful when dealing with file I/O, working with file paths in a cross-platform way, and ensuring that your code behaves consistently across different operating systems.