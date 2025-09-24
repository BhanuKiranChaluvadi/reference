# ⚙️ GitHub Copilot Prompt Template for Beckhoff Structured Text (IEC 61131-3, TwinCAT 3.1+)

## 🚀 Task

Generate **Beckhoff Structured Text (ST)** code for **TwinCAT 3.1+** that meets enterprise software standards.  
Focus strictly on **core logic**. Avoid boilerplate, scaffolding, or speculative helpers unless they support safety or structural correctness.

---

## 🛡️ 1. Safety, Error Handling & Recovery (Top Priority)

- Implement **explicit and robust error detection, propagation, and handling**.
- Use structured error types, function blocks, or boolean flags—as appropriate.
- Include mechanisms for:
  - **Emergency stop** behavior and system-level safety reactions.
  - **Safe shutdown fallback** in all error paths.
  - **System reset** logic that clearly restores safe operating state.

---

## 🔄 2. Initialization Pattern

- Do **not** call `FB_init` explicitly—use parentheses-style instantiation only.
- Place all setup logic inside a `Configure()` method.
- Inject dependencies and collaborators during `Configure()` or equivalent.
- Avoid runtime checks for initialization in cyclic logic.

---

## 🧠 3. Design Principles

- Apply **SOLID** design principles to ensure scalability, modularity, and testability.
- Prioritize:
  - **Composition** over inheritance.
  - **Dependency injection** for flexibility and separation of concerns.
- Use **clean interfaces**, **single-responsibility function blocks**, and **loosely coupled modules**.
- Employ design patterns (e.g., Strategy, State) only when clearly applicable.

---

## 🧪 4. Testability

- All logic must be **modular and independently testable**.
- Avoid tight coupling to I/O or hardware interfaces—prefer abstraction.
- Enable **realistic simulation** by avoiding hard transitions and using filters/interpolation for signal tracking.

---

## 🧼 5. Maintainability

- Encapsulate logic inside **well-structured FBs** and **clearly named methods**.
- Avoid magic numbers—use named constants.
- Keep internal logic **clean, reusable, and self-contained**.

---

## 📝 6. Documentation & Comments

- Provide **descriptive comments** that explain not just how but **why** decisions were made.
- Document assumptions, safety mechanisms, and error paths.

---

## 🚫 7. Syntax & Code Rules

- ❌ No `VAR_IN_OUT`.
- ❌ No logic directly in FB body—**always use PUBLIC/PRIVATE methods**.
- ❌ No optional parameters—**always explicitly specify all arguments**.
- ✅ Method return pattern:
  ```code
  FunctionName := result;
  RETURN;
  ```

- ✅ Use `END_METHOD` after method implementation.
- ✅ Use tab space for method implementation.


The operator __ISVALIDREF can only be used for operands of type REFERENCE TO. This operator cannot be used for checking interface variables. To check whether an interface variable was already assigned a function block instance, you can check the interface variable for not equal to 0 (IF iSample <> 0 THEN …).


No Explicit calling og FB_init. All parameters defined in FB_init must be passed during the function block varaible initilization. This is Beckhoff structured text constraint


