# General Guidance

## General

Don't convert CRLF to LF; keep everything LF always. Even in Windows.

## Sync v Async

Pure business rules: sync where possible. Anything that talks to the outside world: async at the boundary.
