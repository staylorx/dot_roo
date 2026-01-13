# General Guidance

## General

Don't convert CRLF to LF; keep everything LF always. Even in Windows.

## Sync v Async

Pure business rules: sync where possible. Anything that talks to the outside world: async at the boundary.

## CleanArch Projection Handles

If you use projection handle classes, you may _never_ put handles in the domain entities. These are usually situated as a concreate class in the related repository file in the domain.
