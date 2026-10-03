# Specialist Node Contract Specification

Every node invoked by Personal Maestro must adhere to this input/output protocol.

## Input: Briefing Pack
Passed via stdin or isolated prompt context:
```json
{
  "card_id": "string",
  "board": "string",
  "task": "string",
  "settled_facts": {},
  "constraints": [],
  "max_steps": 10
}
```

## Output: Report Block
The node must conclude its execution with a valid YAML/JSON report block:
```yaml
---
status: "done" # enum: "done" | "staged" | "needs-jake" | "blocked-external"
summary: "Single crisp declarative sentence describing what was produced."
artifacts:
  - path: "drafts/heat-pump-rebates.md"
    description: "Federal & PUD rebate analysis table"
blocker: null
proposed_actions:
  - "Approve draft email to Puget Sound Energy certified contractor"
---
```
