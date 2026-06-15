---
trigger: always_on
---
# SAP CLOUD DEV RULES (STRICT)

**1. SKILL ROUTING:** MUST read `SKILLS_ROUTER.md` before any task to dynamically load required skills.
**2. SCOPE & SAFETY:**
- **Consent First:** Ask explicitly before any CUD operations.
- **Custom Only:** Modify ONLY Z/Y objects. NEVER touch Standard Objects.
- **Strict Scope:** Touch ONLY objects in the current task scope. NO unintended side-effects.
- **Collision Check:** Verify object names globally (Z*) before creation. If exists, propose new name and ask for approval.
- **TR & Package:** Required for all new/modified objects. Ask if missing.
- **Read-Only Data:** Business data is READ-ONLY unless explicitly testing RAP BOs.
**3. CODE STANDARDS:**
- **Modern ABAP & OOP:** Enforce Modern ABAP (VALUE, COND, REDUCE) and GoF Patterns. Reject legacy procedural code.
- **Clean Core (Read):** CDS Views ONLY. NEVER SELECT from physical tables.
- **Clean Core (Write):** ABAP EML or Released APIs ONLY. NEVER direct INSERT/UPDATE.
**4. WORKFLOW & FILES:**
- **Scratchpad:** MUST draft complex architecture in a scratchpad first.
- **File Organizer:** 
  - FS inputs -> `fs_docs/`
  - Output TS -> `generated_docs/technical_specifications/`
  - Scratchpads -> `generated_docs/scratchpads/`
  - Walkthroughs -> `generated_docs/walkthroughs/`
  - *NEVER output to `.agents/` or root.*
**5. VALIDATION & ERRORS:**
- **Activation:** Remind/trigger activation. On failure, extract exact SAP error (DO NOT guess).
- **Final Audit:** Post-CUD, perform boundary check: verify no external mutations, syntax-error-free, properly activated, and isolated.