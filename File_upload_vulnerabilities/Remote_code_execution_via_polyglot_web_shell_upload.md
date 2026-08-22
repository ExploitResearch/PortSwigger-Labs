# Remote code execution via polyglot web shell upload

### Goal -

Upload a polyglot file that is both a valid image and a valid PHP web shell to achieve remote code execution.

### Exploitation

1. Create a polyglot file that is valid as both an image and PHP code
2. Use a tool like `exiftool` or manual crafting to embed PHP in image metadata
3. Upload the polyglot file
4. Access the uploaded file to trigger PHP execution
