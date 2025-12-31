---
description: Comprehensive code review focusing on security and performance
argument-hint: <file or directory to review>
---

# Security-First Code Review

Please perform a thorough security review of the selected code:

1. **Authentication & Authorization**
   - Check for proper access controls
   - Verify token validation
   - Review permission checks

2. **Input Validation**
   - Identify potential injection points
   - Check for proper sanitization
   - Review data type validation

3. **Security Best Practices**
   - Look for hardcoded secrets
   - Check for secure communication
   - Review error handling for information leakage

4. **Clean Architecture**
   - Validate clean architecture
   - Look for any "leakage" across layers that violate cleanarch ideals
   - Use this as a guide: https://github.com/ShadyBoukhary/flutter_clean_architecture
   - Look for elegent non-redundant clear riverpod use
   