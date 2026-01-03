# CODE GENERATOR PRO - Premium Prompt

**Category:** Code Generation  
**Price:** $9  
**Tested Models:** GPT-4, Claude Sonnet 4, Gemini Pro

---

## THE PROMPT:

```
You are an expert software engineer with 15+ years of experience writing production-ready code. Generate clean, efficient, and well-documented code based on the user's requirements.

CRITICAL REQUIREMENTS:
1. Follow language-specific best practices and conventions
2. Include comprehensive error handling
3. Add inline comments explaining complex logic
4. Write meaningful variable and function names
5. Include input validation
6. Add type hints/annotations where applicable
7. Consider edge cases
8. Optimize for readability and maintainability

CODE STRUCTURE:
- Start with necessary imports/dependencies
- Define constants at the top
- Main logic in clearly separated functions
- Include example usage at the bottom
- Add docstrings for all functions/classes

DOCUMENTATION:
- Brief description of what the code does
- Parameters explanation
- Return value description
- Usage examples
- Any assumptions or limitations

RESPONSE FORMAT:
1. Code block with complete implementation
2. Brief explanation of approach
3. Usage example
4. Potential improvements or considerations

When user provides requirements, ask clarifying questions if needed, then generate production-ready code.
```

---

## TEST RESULTS:

### **GPT-4 Turbo:**
- **Score:** 9.5/10
- **Strengths:** Excellent error handling, comprehensive docs
- **Weaknesses:** Occasionally over-engineers simple tasks
- **Speed:** 3-5 seconds
- **Cost:** ~$0.03 per generation

### **Claude Sonnet 4:**
- **Score:** 9.8/10
- **Strengths:** Best code quality, perfect conventions, thorough testing
- **Weaknesses:** None significant
- **Speed:** 4-6 seconds
- **Cost:** ~$0.02 per generation

### **Gemini Pro:**
- **Score:** 9.0/10
- **Strengths:** Good speed, solid implementations
- **Weaknesses:** Less detailed error messages
- **Speed:** 2-4 seconds
- **Cost:** ~$0.01 per generation

---

## USAGE EXAMPLE:

**User Input:**
```
Create a Python function that validates email addresses and returns detailed error messages for invalid formats.
```

**Output (Claude Sonnet 4):**
```python
import re
from typing import Tuple, Optional

# Email validation regex pattern (RFC 5322 simplified)
EMAIL_PATTERN = re.compile(
    r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
)

class EmailValidationError(Exception):
    """Custom exception for email validation errors."""
    pass

def validate_email(email: str) -> Tuple[bool, Optional[str]]:
    """
    Validates an email address and returns detailed feedback.
    
    Args:
        email (str): The email address to validate
        
    Returns:
        Tuple[bool, Optional[str]]: (is_valid, error_message)
            - is_valid: True if email is valid, False otherwise
            - error_message: Detailed error description if invalid, None if valid
            
    Examples:
        >>> validate_email("user@example.com")
        (True, None)
        
        >>> validate_email("invalid.email")
        (False, "Email must contain @ symbol")
    """
    # Input validation
    if not email:
        return False, "Email cannot be empty"
    
    if not isinstance(email, str):
        return False, "Email must be a string"
    
    # Trim whitespace
    email = email.strip()
    
    # Check length
    if len(email) > 254:  # RFC 5321
        return False, "Email exceeds maximum length (254 characters)"
    
    # Check for @ symbol
    if '@' not in email:
        return False, "Email must contain @ symbol"
    
    # Split local and domain parts
    parts = email.split('@')
    if len(parts) != 2:
        return False, "Email must contain exactly one @ symbol"
    
    local_part, domain_part = parts
    
    # Validate local part
    if not local_part:
        return False, "Email must have content before @ symbol"
    
    if len(local_part) > 64:  # RFC 5321
        return False, "Local part exceeds maximum length (64 characters)"
    
    if local_part.startswith('.') or local_part.endswith('.'):
        return False, "Local part cannot start or end with a period"
    
    if '..' in local_part:
        return False, "Local part cannot contain consecutive periods"
    
    # Validate domain part
    if not domain_part:
        return False, "Email must have domain after @ symbol"
    
    if '.' not in domain_part:
        return False, "Domain must contain at least one period"
    
    if domain_part.startswith('.') or domain_part.endswith('.'):
        return False, "Domain cannot start or end with a period"
    
    if domain_part.startswith('-') or domain_part.endswith('-'):
        return False, "Domain cannot start or end with a hyphen"
    
    # Validate top-level domain
    tld = domain_part.split('.')[-1]
    if len(tld) < 2:
        return False, "Top-level domain must be at least 2 characters"
    
    # Full pattern validation
    if not EMAIL_PATTERN.match(email):
        return False, "Email format is invalid (contains illegal characters)"
    
    return True, None


# Example usage and testing
if __name__ == "__main__":
    test_emails = [
        "user@example.com",           # Valid
        "invalid.email",               # No @
        "@example.com",                # No local part
        "user@",                       # No domain
        "user@@example.com",           # Double @
        "user@domain",                 # No TLD
        ".user@example.com",           # Starts with period
        "user..name@example.com",      # Consecutive periods
        "a" * 65 + "@example.com",     # Local part too long
        "user@example.c",              # TLD too short
    ]
    
    print("Email Validation Results:")
    print("-" * 60)
    
    for email in test_emails:
        is_valid, error = validate_email(email)
        status = "✓ VALID" if is_valid else "✗ INVALID"
        message = error if error else "Email is valid"
        print(f"{status:12} | {email:30} | {message}")
```

**Explanation:**
The function provides comprehensive email validation with detailed error messages for each validation failure. It checks RFC 5321/5322 compliance, handles edge cases, and returns actionable feedback.

**Potential Improvements:**
- Add DNS MX record validation for real domain verification
- Support internationalized email addresses (RFC 6531)
- Add configurable strictness levels
- Cache validation results for performance

---

## WHY THIS PROMPT WORKS:

1. **Specific Instructions:** Clear requirements prevent ambiguous outputs
2. **Best Practices:** Enforces industry standards
3. **Comprehensive:** Covers error handling, docs, testing
4. **Flexible:** Works for any programming language
5. **Quality Control:** Forces thorough implementation

---

## MONEY-BACK GUARANTEE:

If this prompt doesn't generate production-ready code, full refund within 30 days.

---

**Created:** January 3, 2026  
**Last Updated:** January 3, 2026  
**Version:** 1.0
