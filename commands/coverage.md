---
description: Identify missing test coverage
---

Analyze the current test coverage and:
- Identify untested code paths
- Suggest additional test cases
- Find edge cases not covered
- Recommend integration tests
- Check for proper error testing
- genhtml is available on this system so use it instead of attempting to parse lcov.info
- Do not attempt to read lcov.info directly. It is too large.
