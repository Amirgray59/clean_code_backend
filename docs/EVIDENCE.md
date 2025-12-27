# Evidence — Stage 1 (Clean Code & Architecture)

This document provides concrete evidence for the Stage 1 requirements.
All references include file paths and specific responsibilities to enable fast review.

---

## 1. Clean Architecture & Layered Design

**Evidence**
- Domain logic is fully isolated from the API layer.
- Dependency direction is strictly `api → domain`.

**Files**
- `app/domain/gilded_rose.py`
- `app/api/handlers.py`

**Notes**
- The domain module has no imports from `api`, frameworks, or IO.
- The API layer only performs data mapping and delegates behavior to the domain.

---

## 2. Refactored Domain Logic (Clean Code)

**Evidence**
- Deeply nested conditionals were replaced with small, intention-revealing functions.
- Each function represents a single business rule.

**Files & Examples**
- `update_normal_item` — normal item degradation  
  (`app/domain/gilded_rose.py`)
- `update_aged_brie` — increasing quality rule
- `update_backstage` — tiered quality increase rules
- `handle_expired_item` — centralized expired-item behavior

**Notes**
- Each rule is independently readable and testable.
- No dispatch table was introduced to preserve explicit control flow and clarity.

---

## 3. Explicit Invariants

**Evidence**
- Invariant behavior for special items is enforced explicitly.

**Files**
- `app/domain/gilded_rose.py`

**Examples**
- Sulfuras items short-circuit update logic and never change:
  ```python
  if item.name == SULFURAS:
      continue


## 4. Coverage Report 

=========================================================== tests coverage 
__________________________________________ coverage: platform linux, python 3.13.7-final-0 ___________________________________________

Name                        Stmts   Miss  Cover   Missing
---------------------------------------------------------
app/api/__init__.py             0      0   100%
app/api/handler.py              9      2    78%   4-5
app/domain/__init__.py          0      0   100%
app/domain/gilded_rose.py      52      2    96%   43, 79
app/main.py                     7      7     0%   1-11
---------------------------------------------------------
TOTAL                          68     11    84%
========================================================= 21 passed in 0.05s 
