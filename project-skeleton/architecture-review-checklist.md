# Architecture Review Checklist

Use this checklist as the second pair of eyes in PR review and design review.

## 1. 4-Eyes Principle
- Can another engineer understand the flow in under 5 minutes?
- Is the business path traceable end to end?
- Are retries, duplicates, and failure paths visible?
- Are auth, data access, and side effects explicit?

## 2. SOLID
- one module, one clear responsibility
- business logic depends on abstractions, not framework details
- interfaces stay narrow and role-specific

## 3. DRY
- deduplicate only stable logic
- do not create giant shared `utils` or base classes too early

## 4. YAGNI
- no speculative layers
- no workflow engines unless the problem actually needs them

## 5. KISS
- prefer direct flows
- prefer small modules
- prefer explicit naming and ownership
