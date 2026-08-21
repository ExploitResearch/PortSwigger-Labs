# Path/Directory traversal

### Path traversal

Path traversal, also known as directory traversal, is a web security vulnerability that allows attackers to access files and directories on a web server beyond their intended reach by manipulating user input that is used to construct file paths, essentially tricking the server into accessing unauthorized locations.

Directory traversal vulnerabilities happen when a malicious user can include an arbitrary file path in user input and use special characters to access files from a different directory on the server. Special characters used for this are dot-dot-slash combinations: *../* for Linux/UNIX or *..\* for Windows. These combinations allow access to parent directories from a relative path.

The only direct consequence of a directory traversal attack is access to sensitive information. This sensitive information may be used directly or to follow up with other attacks. If there is sensitive information stored in files on the server, for example, confidential photos of documents or sensitive data in text files, the attacker can find and access such files.

### How Path Traversal Works:

  1. **User Input:**
    - The web application takes user input, often in the form of a file path or filename.
  1. **Lack of Validation:**
    - The application does not properly validate or sanitize the user input, allowing it to include special characters or sequences.
  1. **Traversal Attempts:**
    - An attacker submits input containing "../" or other path traversal sequences to navigate up the directory tree.
  1. **File Access:**
    - If the input is not properly sanitized, the application constructs a file path that goes beyond the intended directory, allowing the attacker to access unauthorized files.
### Example:

Consider a URL parameter used to load user-specific files:

```html
https://example.com/viewProfile?file=user123_profile.txt
```

An attacker might attempt to traverse directories by manipulating the parameter:

```text
https://example.com/viewProfile?file=../../../../../etc/passwd
```

If the application does not properly validate the input, this could result in the attacker accessing sensitive system files.

### Mitigation Strategies for Path Traversal:

  1. **Input Validation and Sanitization:**
    - Properly validate and sanitize user input to ensure it adheres to expected formats and does not contain malicious characters.
  1. **Use Whitelists:**
    - Define a whitelist of allowed characters or patterns and validate user input against this whitelist.
  1. **File Path Normalization:**
    - Normalize file paths before processing them to eliminate unnecessary elements (e.g., "../../") and ensure a consistent format.
  1. **Use Absolute Paths:**
    - Avoid using user input to construct relative paths. Prefer absolute paths or store files in a designated location.
  1. **Application Hardening:**
    - Configure the web server and application to run with the least privilege necessary to limit the potential impact of a successful path traversal attack.
> 💡

    1. Avoid passing any filenames in user input. This includes not just direct user input but also other data sources that can be manipulated by the attacker, for example, cookies.
    1. If your application requires you to use filenames from user input and there is no way around it, create a whitelist of safe files.
    1. If you cannot create a whitelist because you use arbitrary filenames, for example, if users upload the files, store filenames in the database and use table row identifiers in user input. You can also use URL mappings to identify files with no risk of path traversal.
### There are three main types of paths: Default, Absolute, and Relative.

  1. **Default Path:**
    - A default path typically refers to the location where an application or system looks for files if no specific path is provided. It's the assumed or predefined location.
    - The default path is often determined by the operating system or the application itself.
    - Example (on Windows): `C:\Program Files\Application\file.txt`
    - Example (on Unix-like systems): `/usr/local/bin/file`
  1. **Absolute Path:**
    - An absolute path provides the full and specific location of a file or directory from the root of the file system.
    - It starts from the root directory and includes all the directories leading to the target file or directory.
    - Always provides a fixed and unambiguous location.
    - Example (on Windows): `C:\Users\Username\Documents\file.txt`
    - Example (on Unix-like systems): `/home/username/Documents/file`
  1. **Relative Path:**
    - A relative path specifies the location of a file or directory relative to the current working directory.
    - It does not start from the root directory; instead, it is based on the current location.
    - Can be more concise and portable, as it adapts to changes in directory structure.
    - Example: If the current directory is `/home/username/Documents/`, a relative path to `file.txt` might be `../Downloads/file.txt`.
    - Special notations like `..` (parent directory) and `.` (current directory) are used in relative paths.
> 💡 **Examples:**

      - Default path: `C:\Program Files\Application\file.txt`
      - Absolute path: `/home/username/Documents/file`
      - Relative path: `../Downloads/file.txt` (relative to `/home/username/Documents/`)
> 

    - Avoid passing any filenames in user input. This includes not just direct user input but also other data sources that can be manipulated by the attacker, for example, cookies.
    - If your application requires you to use filenames from user input and there is no way around it, create a whitelist of safe files.
    - If you cannot create a whitelist because you use arbitrary filenames, for example, if users upload the files, store filenames in the database and use table row identifiers in user input. You can also use URL mappings to identify files with no risk of path traversal.
### Certain sensitive files on Linux-based web servers

Here are some files that are often the target of directory traversal attacks on Linux-based web servers. All these files are always readable by all operating system users:

  - */proc/version* – contains the version of the Linux kernel running on the system. This information allows the attacker to find exploits for that particular Linux kernel.
  - */proc/mounts* – contains a list of currently mounted file systems. This allows the attacker to try to access these file systems, for example, through follow-up directory traversal attacks.
  - */proc/net/arp* – contains the address resolution protocol (ARP) table, which could be used to discover other connected systems (potential attack targets).
  - */proc/net/tcp* and */proc/net/udp* – contain lists of ongoing TCP/UDP connections, which could be used to discover other connected systems (again, potential attack targets).
## [File path traversal, simple case](./File_path_traversal,_simple_case.md)

## [File path traversal, traversal sequences blocked with absolute path bypass](./File_path_traversal,_traversal_sequences_blocked_with_absolute_path_bypass.md)

## [File path traversal, traversal sequences stripped non-recursively](./File_path_traversal,_traversal_sequences_stripped_non-recursively.md)

## [File path traversal, traversal sequences stripped with superfluous URL-decode](./File_path_traversal,_traversal_sequences_stripped_with_superfluous_URL-decode.md)

## [File path traversal, validation of start of path](./File_path_traversal,_validation_of_start_of_path.md)

## [File path traversal, validation of file extension with null byte bypass](./File_path_traversal,_validation_of_file_extension_with_null_byte_bypass.md)

