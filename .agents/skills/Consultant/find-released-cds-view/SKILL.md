---
name: find-released-cds-view
description: Find the best SAP released CDS view (DDLS) for a RAP/reporting field by matching the user's business object, screen context, required data grain, field availability, and local data coverage, using S/4HANA Cloud Public Edition (`public_cloud`) as the default mcp-sap-docs target. Use when asked to map a business field from SAP screens such as Business Partner, Customer, Sales Area, Company Code, Address, or Communication to a released clean-core CDS source, value help, text view, or cloud-ready alternative.
---

# Find Released CDS View

Find the released CDS view that best fits the business meaning and result shape the user needs. Use S/4HANA Cloud Public Edition as the baseline, prefer released APIs, and verify local fields/readability when SAP/ADT access is available.

The screen path helps identify the business field, but the final recommendation must also match the required data grain and local data coverage. A child communication/address view can be semantically precise but still be wrong for a customer-level report if it returns too few rows; in that case prefer a released customer-level view such as `I_CUSTOMER` when it exposes the needed field.

## Smart Defaults

| Setting | Default | Rationale |
|---|---|---|
| Object type | `DDLS` | CDS views/view entities are DDLS objects in release-state data |
| Release state | `released` | RAP clean-core reuse should prefer released APIs |
| Clean Core level | `A` | Level A is released API only |
| System type | `public_cloud` | Use the strictest S/4HANA Cloud Public released-API baseline by default |
| Candidate count | 5-10 verified views | Avoid dumping long search result lists |
| Verification | Always verify exact object details and local SAP readability | Generic released status is not enough |
| Recommendation | Prefer the view with the right grain and enough data coverage | Screen-node precision alone is not sufficient |

## Input

The user may provide any of:
- A business topic: "sales order", "purchase requisition", "journal entry"
- An unreleased object to replace: `VBAK`, `MARA`, `I_SomeInternalView`
- A RAP usage context: root entity, child entity, value help, validation lookup, determination lookup, read-only projection
- A screen path: Business Partner role/tab/section/field
- A result shape: one row per customer, one row per address, one row per sales area, value help list, text/description lookup
- A target system context, only if they explicitly want something other than S/4HANA Cloud Public

If the user gives only a broad topic, proceed with search and state assumptions. Ask a question only if the business meaning is ambiguous enough that wrong candidates would be misleading.

## Step 1: Set Target Context

Default the release-state search target to:

```
system_type="public_cloud"
clean_core_level="A"
state="released"
object_type="DDLS"
```

Do not read `system-info.md` and do not probe the SAP system just to choose a release-state target. Use a different `mcp-sap-docs` `system_type` only when the user explicitly asks for another target:

| SAP context | `mcp-sap-docs` system_type |
|---|---|
| S/4HANA Cloud Public Edition | `public_cloud` |
| SAP BTP ABAP Environment / Steampunk | `btp` |
| S/4HANA Cloud Private Edition | `private_cloud` |
| S/4HANA on-premise | `on_premise` |

Local SAP/ADT tools are still useful after discovery to confirm that a candidate DDLS exists and is readable in the connected system, but they are not required to determine the default search target.

## Step 2: Turn User Context Into Search Terms

Build 3-6 focused search terms:

- Exact object names from the user, if any
- Business noun phrases: "sales order", "purchase order item", "business partner"
- Common SAP object stems: `I_SALESORDER`, `I_PURCHASEORDER`, `I_BUSINESSPARTNER`
- Application component, if known: `SD-SLS`, `MM-PUR`, `FI-GL`
- Replacement source terms from unreleased tables/views: table name plus business name

Prefer CDS naming patterns based on RAP usage:

| RAP use | Prefer |
|---|---|
| BO data source / association target | `I_*` interface or composite views |
| Value help | `I_*VH`, `C_*VH`, or released value-help specific views |
| Read-only UI/analytics | `C_*` consumption/query views if released and suitable |
| API integration | Released API/interface views with matching business object semantics |

Do not assume a table-like name maps to a released CDS view. Search and verify.

## Step 2b: Determine Business Grain

Before recommending a view, infer the grain the user needs:

| User wording / goal | Preferred grain | Typical view family |
|---|---|---|
| "of customer", "for all customers", one row per customer | Customer | `I_CUSTOMER` |
| Customer > Sales and Distribution / Sales Area fields | Customer + Sales Area | `I_CUSTOMERSALESAREA` |
| Customer > Fin.Accounting / Company Code fields | Customer + Company Code | `I_CUSTOMERCOMPANY` |
| Business Partner (Gen.) > Address fields | Business Partner + Address | `I_BUSINESSPARTNERADDRESSTP_3` |
| Address > Communication child records | Business Partner + Address + communication record | `I_BUSPART*TP_3` communication views |
| Code + description only | Code/text lookup | `I_*` master plus `I_*TEXT` |

Treat screen path as a clue, not an automatic source choice. If a screen field also exists directly on a higher-level released view that matches the user's requested output grain, prefer the higher-level view.

Example: if the user asks for "Zalo/mobile number of customer" and expects a complete customer list, prefer `I_CUSTOMER.TelephoneNumber2` when it has coverage. Use `I_BUSPARTMOBILEPHONENUMBERTP_3` only when the user needs actual BP address communication records or the customer-level field is not suitable.

## Step 3: Search Released DDLS Objects

Use `mcp-sap-docs` release-state search:

```
mcp__abap_docs.sap_search_objects(
  query="<business term or object stem>",
  system_type="public_cloud",
  clean_core_level="A",
  object_type="DDLS",
  state="released",
  limit=25
)
```

If the result set is too broad:
- Add `app_component` when known.
- Search exact stems such as `I_SALESORDER` instead of broad phrases.
- Page with `offset` only when the first page has plausible partial matches.

If no results are found:
- Try exact SAP naming stems from the business domain.
- Try a neighboring application component.
- Search documentation with `mcp__abap_docs.search` for the business object name plus "CDS view released API".
- Report that no released DDLS candidate was found under the chosen target system and Clean Core level before widening to level `B`.

## Step 4: Verify Each Candidate

For each plausible candidate, first verify release-state details:

```
mcp__abap_docs.sap_get_object_details(
  object_type="DDLS",
  object_name="<candidate>",
  system_type="public_cloud",
  target_clean_core_level="A"
)
```

Reject or downgrade candidates when:
- `found` is false
- `state` is not `released`
- `cleanCoreLevel` is not `A` for BTP/public cloud targets
- The application component is clearly outside the user's domain
- The object has a successor and the successor is a better fit

Then verify usability in the actual SAP system:

```
SAPRead(type="DDLS", name="<candidate>")
SAPRead(type="API_STATE", name="<candidate>", objectType="DDLS")
```

If available, inspect fields and dependencies:

```
SAPContext(type="DDLS", name="<candidate>", action="deps")
```

Mark a candidate as "released but not locally usable" if the local system cannot read it, does not contain it, or the current user lacks access.

## Step 5: Check RAP Fit

Evaluate the verified DDLS source against the intended RAP use:

- Grain: keys match the intended result level; avoid child views that drop or multiply rows when the report is customer-level
- Key fields: stable and sufficient for association or root/child identity
- Required fields: contains the business fields the user needs
- Coverage: local data has enough rows for the user's population; do not choose a semantically precise child view if it only covers a small subset and the user needs all customers
- Associations: useful released associations exist and are readable
- Cardinality: compatible with intended RAP associations
- Parameters: avoid parameterized CDS views for simple RAP entity sources unless the use case requires them
- Analytical/query semantics: do not use analytics-only views as transactional BO sources unless explicitly read-only
- Authorization: note DCL/access-control implications if visible in source or context

If the user wants to use a candidate in a new custom CDS view, provide a minimal source example only after confirming the candidate fields from the local system.

## Step 6: Present Results

Return a concise table:

| Rank | CDS view | Status | Why it fits | Caveats |
|---|---|---|---|---|
| 1 | `I_SALESORDER` | Released, locally readable | Sales order header, SD-SLS, useful key fields | Header only; item data needs separate view |

Then recommend one primary candidate and explain:
- Target system type and Clean Core level used
- MCP release-state evidence
- Local SAP verification result
- Why the selected view grain matches the requested output
- Any coverage tradeoff versus more semantically specific child views
- How to use it in RAP: source view, association target, value help, or lookup

## Failure Modes

| Situation | Response |
|---|---|
| `mcp-sap-docs` search returns no useful DDLS | State the searched terms/system type and try exact stems or app component filters |
| Candidate is released in docs but missing locally | Explain that release-state repository and installed system content differ; do not recommend it as usable |
| User lacks DDLS read authorization | Report release status separately from local usability |
| Only unreleased/internal views fit | Offer released alternatives if any, otherwise state that no clean-core released CDS view was found |
| Broad domain has many candidates | Narrow by RAP role: root data source, item association, value help, analytics, or lookup |
| Screen-node view has poor row coverage | Prefer a released higher-level view with the same field when it matches the requested grain, and document the tradeoff |
