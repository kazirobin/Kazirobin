# OS Module

The `os` module provides you with many useful properties and methods for interacting with the operating system and server.

To use the `os` module, you include it as follows:

```jsx
const os = require('os');
```

## OS Module Properties and Methods

| **Method** | **Description** |
| --- | --- |
| arch() | Returns the operating system CPU architecture |
| constants | Returns an object containing the operating system's constants for process signals, error cotes etc. |
| cpus() | Returns an array containing information about the computer's CPUs |
| endianness() | Returns the endianness of the CPU |
| EOL | Returns the end-of-line marker for the current operating system |
| freemem() | Returns the number of free memory of the system |
| hostname() | Returns the hostname of the operating system |
| loadavg() | Returns an array containing the load averages, (1, 5, and 15 minutes) |
| networkInterfaces() | Returns the network interfaces that has a network address |
| platform() | Returns information about the operating system's platform |
| release() | Returns information about the operating system's release |
| tmpdir() | Returns the operating system's default directory for temporary files |
| totalmem() | Returns the number of total memory of the system |
| type() | Returns the name of the operating system |
| uptime() | Returns the uptime of the operating system, in seconds |
| userInfo() | Returns information about the current user |