# Local Trust-Boundary Template

Use this template when a project needs to make local trust, hosting, and tool restrictions explicit.

This template is **local by design**.
It should not be copied back into framework truth unless a real pattern clearly generalizes.

---

## Project identity

### Project name

### Team or org scope

### Last updated

---

## Data classes

List the data classes that matter locally.

| Data class | Short description | Example content | May leave trust boundary? |
|---|---|---|---|
| Public | Example | marketing copy, public docs | yes |
| Internal | Example | internal planning notes | depends on project rule |
| Restricted | Example | customer or regulated material | usually no |

---

## Model hosting posture

| Model / runtime class | Hosting posture | Allowed data classes | Not allowed for | Notes |
|---|---|---|---|---|
| Externally hosted premium | hosted | public, maybe internal | restricted / regulated | Example only |
| Local runtime | self-hosted | public, internal, restricted | depends on capability limits | Example only |

---

## Tool posture

| Tool class | Default posture | Allowed lanes | Human gate required? | Notes |
|---|---|---|---|---|
| Read tools | allowed | bounded reading / review | no | Example only |
| Write tools | restricted | approved execution lanes | often yes | Example only |
| Outbound tools | tightly restricted | specific low-risk lanes only | maybe | Example only |
| Destructive tools | exceptional | explicit high-control lanes only | yes | Example only |

---

## Lane mapping

Describe how the posture changes by lane.

| Lane / slice type | Data class | Allowed model posture | Allowed tools | Review posture |
|---|---|---|---|---|
| Planning | public / internal | hosted or local | read-only | bounded review |
| Sensitive execution | restricted | local only | tightly restricted | human approval |

---

## Human-gate rules

Examples:

- destructive actions always require explicit human approval
- restricted-context write actions never execute without local review
- model confidence never overrides a blocked trust posture

---

## Exceptions and durable local decisions

Record exceptions explicitly.

Examples:

- one externally hosted model may be used for a specific public-only lane
- one tool is temporarily disabled pending review
- one integration requires manual confirmation until verification improves

---

## Notes

Keep this template local.
It should describe the real trust posture of the project,
not the idealized posture of the framework.
