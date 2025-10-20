------------------------------------------------------------------------------
  TwinCAT Structured Text Coding Principles
  (IEC 61131-3 / Beckhoff)
------------------------------------------------------------------------------

  CORE DESIGN RULES
  -----------------
  - Write BARE-MINIMUM, ESSENTIAL-ONLY code — no optional or decorative code.
  - Prioritize LOGICAL CORRECTNESS first; avoid premature optimization.
  - Keep code SIMPLE, CLEAR, and MINIMAL — follow KISS, YAGNI, and DRY.
  - Maintain SEPARATION OF CONCERNS — one function block or method = one purpose.
  - Use COMPOSITION and DEPENDENCY INJECTION instead of direct initialization.
  - Code must be MEMORY-EFFICIENT, EXPANDABLE, and MAINTAINABLE.

  MEMORY & RESOURCE SAFETY
  ------------------------
  - Ensure MEMORY SAFETY and check for RAII issues.
  - Avoid unnecessary copies, allocations, or pointer misuse.
  - Manage object lifetimes and cleanup deterministically.

  CODE STYLE
  ----------
  - Keep consistent NAMING and FORMATTING.
  - Avoid long lines, nested logic, and redundant comments.
  - Use concise, PRODUCTION-RELEVANT comments only — no temporal or debug notes.

  FUNCTION BLOCK INITIALIZATION AND EXIT
  --------------------------------------
  - Always use the correct TwinCAT method signatures:

      METHOD FB_init : BOOL
      VAR_INPUT
          bInitRetains : BOOL; // TRUE = retain variables initialized (warm/cold start)
          bInCopyCode  : BOOL; // TRUE = instance moved into copy code (online change)
      END_VAR

      METHOD FB_exit : BOOL
      VAR_INPUT
          bInCopyCode : BOOL; // TRUE = exit method called when copied (online change)
      END_VAR

  - If a Function Block defines FB_init:
      * ALL parameters must be explicitly specified during the declaration.
      * No default values are allowed, EXCEPT for bInitRetains and bInCopyCode.
      * FB_init must NOT be called explicitly — it is called implicitly
        during object declaration.

  TWINCAT / BECKHOFF SPECIFIC NOTES
  ---------------------------------
  __QUERYINTERFACE
    - Converts one interface reference to another at runtime.
    - Returns BOOL (TRUE = success).
    - Syntax:  __QUERYINTERFACE(<ITF_Source>, <ITF_Dest>);
    - To enable querying, the Function Block must EXTEND __System.IQueryInterface.

  __QUERYPOINTER
    - Converts an interface reference to a pointer at runtime.
    - Returns BOOL (TRUE = success).
    - Syntax:  __QUERYPOINTER(<ITF_Source>, <Pointer_Dest>);

  ADDITIONAL NOTES
  ----------------
  - TO_PVOID does not exist in TwinCAT.
  - An interface variable can directly reference a function block 
    that implements the interface.
  - __QUERYINTERFACE cannot be used with POINTER TO BYTE, 
    since dereferencing yields BYTE, not a function block instance.

  SUMMARY
  --------
  When writing TwinCAT Structured Text code:
    * Write BARE-MINIMUM, ESSENTIAL-ONLY code.
    * Focus on LOGICAL CORRECTNESS, SIMPLICITY, and MAINTAINABILITY.
    * Apply KISS, YAGNI, DRY, and SINGLE RESPONSIBILITY principles.
    * Ensure MEMORY SAFETY and consistent NAMING.
    * Prefer DEPENDENCY INJECTION and COMPOSITION.
    * Use correct FB_init / FB_exit signatures and initialization rules.
    * Use __QUERYINTERFACE and __QUERYPOINTER correctly;
      ensure the FB EXTENDS __System.IQueryInterface.
    * Avoid unsupported conversions like TO_PVOID or POINTER TO BYTE.

------------------------------------------------------------------------------
