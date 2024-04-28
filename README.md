# Folder Permissions in Web Applications

This documentation is designed to explain the folder permissions required for a secure and functional web application.

## Overview
Managing folder permissions in web applications is crucial for ensuring security and proper access control. Incorrect permissions can lead to unauthorized access or data exposure, while overly restrictive permissions can hinder the functionality of the application. This document provides a clear and detailed explanation of how to set and manage folder permissions effectively. 

## Understanding Permissions

In Unix-like operating systems, each file or folder has associated permissions that control the actions users can perform on it. 

There are three types of permissions:

  - **Read** (r): Allows the contents of the file or directory to be read.
  - **Write** (w): Allows writing or modifying the file or directory.
  - **Execute** (x): Allows execution of the file as a program or script; for directories, it allows users to enter the directory and access its contents.

These permissions can be assigned to three different types of users:

  - **Owner** (u): The user who created the file or directory.
  - **Group** (g): Users who are part of a defined group.
  - **Others** (o): Any other users on the system.
  
_These permissions affect the security and functionality of web applications and need to be carefully managed._

## Numeric (Octal) and Symbolic Permissions

Permissions can be represented in numeric (octal) or symbolic notation. Here's how each notation maps to file permissions:

| Numeric | Symbolic | Permission Type      | Description                                                                             |
|---------|----------|----------------------|-----------------------------------------------------------------------------------------|
| 7       | rwx      | Read, Write, Execute | Full permissions: Read, write, and execute/traverse the file or directory.              |
| 6       | rw-      | Read, Write          | Read and write the file or directory, but cannot execute/traverse if not executable.    |
| 5       | r-x      | Read, Execute        | Read and execute the file or traverse the directory, but cannot modify it.              |
| 4       | r--      | Read Only            | Read the file or directory only; no modifications or execution allowed.                 |
| 3       | -wx      | Write, Execute       | Modify and execute the file or traverse the directory, but cannot read the content.     |
| 2       | -w-      | Write Only           | Modify the file or directory only; no execution or reading the content.                 |
| 1       | --x      | Execute Only         | Execute/traverse the file or directory only; no reading or modifying the content.       |
| 0       | ---      | No Permission        | No permissions granted. The file or directory cannot be read, modified, or executed.    |

## Permission Types Table

Here is a detailed table of permissions:

| Octal Value | Symbolic Notation | Owner Permissions | Group Permissions | Others Permissions | Description                  |
|-------------|-------------------|-------------------|-------------------|--------------------|------------------------------|
| 777         | rwxrwxrwx         | Read, Write, Exec | Read, Write, Exec | Read, Write, Exec  | No restrictions on permissions. Not recommended for most cases due to security concerns. |
| 755         | rwxr-xr-x         | Read, Write, Exec | Read, Exec        | Read, Exec         | Standard setting for web folders; owners can modify, while others can only read and execute. |
| 750         | rwxr-x---         | Read, Write, Exec | Read, Exec        | No Access          | Owners can modify; selected group can read and execute; others have no access. |
| 700         | rwx------         | Read, Write, Exec | No Access         | No Access          | Only the owner has access. Suitable for sensitive directories. |
| 644         | rw-r--r--         | Read, Write       | Read              | Read               | Standard setting for files where the owner writes and others only read. |
| 640         | rw-r-----         | Read, Write       | Read              | No Access          | Owner can write; group can read; others have no access. Ideal for logs or config files. |
| 600         | rw-------         | Read, Write       | No Access         | No Access          | Only the owner can read and write. Secure setting for configuration files. |

## Best Practices

- Never use `777` for web applications unless absolutely necessary, as it allows everyone to modify and execute files, which poses a serious security risk.
- Use `755` for **folders** and `644` for **files** to allow your web server to read and serve files while preventing unauthorized modifications.
- **Adjust permissions carefully** depending on your specific needs and environment, especially when handling sensitive data.

## License

This guide is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Copyright

© 2024 Ramazan Çetinkaya. All rights reserved.
