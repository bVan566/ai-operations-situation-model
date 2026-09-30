# Sanitized Example Scenario

This example demonstrates routing behavior without using production data.

## Incoming Events

1. A routine customer request arrives and is covered by an approved response process.
2. A scheduled follow-up is due in three days.
3. A proposal is awaiting an external reply.
4. A requested change would alter price and scope.
5. A third-party service reports degraded performance but the business process is still functioning.

## Resulting Situation Model

```yaml
- id: example-001
  summary: Respond to routine customer request
  state: NOW
  owner: operations
  authority: autonomous
  next_action: Follow approved response process
  terminal_condition: Response recorded as successfully sent

- id: example-002
  summary: Customer follow-up
  state: NEXT
  owner: operations
  authority: autonomous
  trigger: Scheduled follow-up date
  terminal_condition: Follow-up completed or state changed

- id: example-003
  summary: Await proposal response
  state: WAITING
  owner: account-owner
  authority: autonomous
  trigger: Customer response or follow-up deadline
  terminal_condition: Response received or opportunity closed

- id: example-004
  summary: Decide requested scope and pricing change
  state: DECISIONS
  owner: authorized-human
  authority: human-only
  next_action: Review commercial impact
  terminal_condition: Decision recorded and routed

- id: example-005
  summary: Third-party service degradation
  state: WATCHING
  owner: operations
  authority: autonomous
  trigger: Service impact crosses defined threshold
  terminal_condition: Service recovers or issue becomes actionable
```

## What This Demonstrates

The same intake stream produces different operational behavior based on dependency, timing, authority, and impact.

The model does not treat every detected event as a task and does not treat every task as permission to act.
