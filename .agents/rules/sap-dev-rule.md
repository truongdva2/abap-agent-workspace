---
trigger: always_on
---

SAP PUBLIC CLOUD DEV RULES & SKILL ROUTING (AUTOMATIC WORKSPACE RULES)
You must follow these rules at all times for this workspace:

SKILL ROUTING (MANDATORY): Before executing any analysis, coding, or system verification task, you MUST read the skill router file: SKILLS_ROUTER.md to discover and dynamically load the exact specialized skills required. Do not load unrelated skills.

CONSENT, CUSTOM & SCOPE ONLY (STRICT):

Ask explicitly before any Create/Update/Delete (CUD).

Modify ONLY Custom Objects (Z/Y). NEVER modify Standard Objects.

[NEW] STRICT SCOPE CONTROL: Interact and modify ONLY the exact objects mentioned in the current task scope. NEVER touch, modify, or reference any unrelated objects, packages, or configurations.

PACKAGE & TR: Every new/modified object requires a Package and Transport Request (TR). If missing, STOP and ask the user.

READ-ONLY DATA: Business data is strictly READ-ONLY. No modifications unless explicitly testing custom RAP BOs with user consent.

CLEAN CORE (STRICT):

Read: Use CDS Views ONLY. NEVER use SELECT directly on physical database tables.

Write: Use ABAP EML or released APIs ONLY. NEVER use direct table updates (INSERT/UPDATE/MODIFY).

ACTIVATION & ERRORS: Always remind/trigger object Activation. If an action fails, extract the exact SAP Error Message; DO NOT guess the cause.

[NEW] USE SCRATCHPAD FOR COMPLEXITY: Before generating large ABAP code blocks or multiple interconnected objects (like RAP models), you MUST draft the architecture in a scratchpad first to prevent errors and save context tokens.

[NEW] FINAL VALIDATION & BOUNDARY CHECK (MANDATORY):

After completing any task involving system modifications (CUD operations, code edits, or activations), you MUST perform a self-audit and automated review.

Run a strict boundary check to detect errors and ensure that absolutely NO unintended side-effects or mutations have occurred on external or unrelated objects.

Verify that all modified objects are syntax-error-free, properly activated, and isolated within the defined scope before reporting success to the user.