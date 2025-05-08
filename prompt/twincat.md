
### 🔧 **Prompt for GitHub Copilot: Generate Beckhoff Structured Text (IEC 61131-3) Code**

Generate Beckhoff Structured Text (ST) code that **strictly adheres** to the following prioritized guidelines, ensuring safety, maintainability, and extensibility:

---

### 🚨 **1. Safety and Error Handling (Top Priority)**
- Safety is **non-negotiable**—always implement robust error handling and status mechanisms.
- Clearly define behaviors for **emergency stop** and **reset** to manage critical conditions reliably.
- Include structured methods for setting, tracking, and retrieving errors.

---

### ⚙️ **2. Initialization Rules**
- Never **explicitly call `FB_init`**.
- Always **pass initialization parameters via parentheses** during variable declaration (this triggers `FB_init` implicitly).
- Avoid performing **repeated initialization checks** in logic—ensure all setup is complete in `FB_init`.
- If initialization logic is needed, place it in a clearly named **`Configure()` method** instead of relying on `FB_init`.

---

### 🧠 **3. Design Principles**
- Follow **SOLID** principles strictly.
- Emphasize **composition** over inheritance; encapsulate sub-behaviors using internal function blocks.
- Adhere to **Separation of Concerns (SoC)**, **DRY**, and **KISS** principles.
- Use **relevant design patterns** where applicable (e.g., Strategy, State).

---

### 🧪 **4. Testing and Simulation**
- Ensure all code is **modular and independently testable**.
- Structure logic to support **simulation and emulation**:
  - Process variables (e.g., temperatures, positions) must **smoothly transition** to setpoints using linear interpolation or filters—**no instant jumps**.

---

### 🧼 **5. Maintainability & Clarity**
- Write **modular**, **reusable**, and **clearly named** methods and variables.
- Avoid magic numbers—use **well-named constants** or enums.
- Solutions must be **simple, readable, and easily extendable**.

---

### 🗣️ **6. Comments and Documentation**
- Include **clear, descriptive comments** for all logic, decisions, and assumptions.
- Comments must help any future developer (or Copilot) understand the purpose of each section.

---

### 🚫 **7. Coding Restrictions & Conventions**
- **Do not use `VAR_IN_OUT`** parameters.
- **Do not place logic** directly inside the function block body—use **PUBLIC**, **PRIVATE**, or **PROTECTED** methods.
- **No optional parameters** in method declarations—always provide all arguments.
- For methods/functions, use `FunctionName := returnValue; RETURN;` — **never use `RETURN returnValue`**.

---

### 📌 **Reminders for Copilot**
- Never call `FB_init` directly.
- Simulate hardware interactions smoothly and logically.
- Prefer structured, safe, and extendable code over brevity or cleverness.
- Maintain **strong separation of responsibilities** within the FB design.

