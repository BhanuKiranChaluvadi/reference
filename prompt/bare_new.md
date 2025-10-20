

### 🧠 **TwinCAT Structured Text Coding Principles (codesys, IEC 61131-3 / Beckhoff)**

**1. Core Design Rules**

* Always write **bare-minimum code** — no optional or decorative code.
* Prioritize **logical correctness** first; avoid premature optimization.
* Keep code **simple, clear, and minimal** — follow **KISS**, **YAGNI**, and **DRY**.
* Maintain **separation of concerns** — one function block or method = one clear purpose.
* Use **composition and dependency injection** instead of direct initialization.
* Code must be **memory-efficient, expandable, and maintainable**.

**2. Memory & Resource Safety**

* Ensure **memory safety** and check for **RAII** (Resource Acquisition Is Initialization) issues.
* Avoid unnecessary copies, allocations, or pointer misuse.
* Manage object lifetimes and cleanup deterministically.

**3. Code Style**

* Enforce **consistent naming** and **clean formatting**.
* Avoid long lines, nested logic, and redundant comments.
* Use **concise, production-relevant comments only** — no temporal or debug notes.

---

### ⚙️ **TwinCAT / Beckhoff Specific Notes**

**`__QUERYINTERFACE`**

* Converts one **interface reference** to another at runtime.
* Returns `BOOL` (`TRUE` = conversion succeeded).
* **Syntax:**

  ```st
  __QUERYINTERFACE(<ITF_Source>, <ITF_Dest>);
  ```

**`__QUERYPOINTER`**

* Converts an **interface reference** to a **pointer** at runtime.
* Returns `BOOL` (`TRUE` = conversion succeeded).
* **Syntax:**

  ```st
  __QUERYPOINTER(<ITF_Source>, <Pointer_Dest>);
  ```

**Additional Notes:**

* `TO_PVOID` **does not exist** in TwinCAT.
* An **interface variable** can **directly reference** a function block implementing the interface.
* `__QUERYINTERFACE` **cannot** be used with `POINTER TO BYTE`, since it dereferences to a `BYTE`, not a function block instance.

---
