# Remote code execution via polyglot web shell upload

### Goal -

Upload a polyglot file that is both a valid image and a valid PHP web shell to achieve remote code execution.

### Vulnerability / Concept

The application validates uploaded files by checking both the Content-Type and file content (magic bytes), but a polyglot file can satisfy both checks while containing executable code.

### Exploitation

1. Create a polyglot file that is valid as both an image and PHP code
2. Use a tool like `exiftool` or manual crafting to embed PHP in image metadata
3. Upload the polyglot file
4. Access the uploaded file to trigger PHP execution

### Why It Works

The application checks file validity by examining the file's magic bytes and Content-Type header. A polyglot file contains valid image headers (satisfying the image check) while also containing PHP code in a location that gets executed when the file is accessed as PHP.

### Key Takeaways

- Validate file content, not just headers
- Store uploaded files outside the web root
- Disable script execution in upload directories
- Use random filenames without preserving extensions
