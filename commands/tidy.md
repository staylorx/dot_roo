---
description: Comprehensive code tidy
---

# Tidy Code Review

Please perform a thorough cleanliness review of the entire codebase:

- You don't need to overthink or sequentially think on any of this.
- No Code style violations
- No Potential bugs
- No Non-idiomatic Dart
- No unamed or positional parameters; must use named parameters always. The only exception are packages that we have not created, or those that have single parameters with parameter names of "ref", "message", or "loggerName".
- Analyze the codebase and ensure there are no errors, warnings, or info problems
- Format the codebase always using `dart format .` Run this again after this mode is finished. Every time
- Ensure everything that might reasonably expect a dartdoc comment has a brief, tight comment.a
- No Dart code in readme, markdown, or memory-bank files. Explain how code works using tests
- Use `stdout.writeln()` for CLI output (/bin folder). Never use print(). Use logging in the src and test code.
- No failing tests
- Ensure all files are in LF, not CRLF. Even in Windows, always LF.
- No unused imports
- If we're using clean architecture, and we almost always are, be sure that's super clean and crisp
- If we're using fpdart, then be sure we're using Failure and Either and full functional programming idioms.
- Repeat myself: no errors, warnings, or info problems. Ever. Fix, then run format again.
- Finally, update memory bank.
