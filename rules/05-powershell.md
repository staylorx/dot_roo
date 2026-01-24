I like Windows. I like developing in Windows. However,

- Never convert files into CRLF, especially existing files. All files always have LF endings.
- Files are always UTF-8, never UTF-8 with BOM.
- Never use powershell commands. Better to create small scripts in Dart to get what you need done. Look for reusability and if a tool looks like a good utility, add it to a tools/ folder in the root of the project.
- all your requests to use powershell will be denied. Work around that.
