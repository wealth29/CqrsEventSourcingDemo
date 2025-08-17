Real-world scenario: Employee Expense Reimbursement (mid-sized company)

Problem: Employees submit expenses (transport, meals, lodging). Finance needs airtight audit trails, policy enforcement (limits, categories), multi-stage approvals, and clean analytics (monthly spend by department, policy violations), plus reliable payout triggers.

How this API fixes it with CQRS + Event Sourcing:

Event Sourcing: Every change is an event (e.g., ExpenseSubmitted, ReceiptAttached, ExpenseApproved, ExpensePaid). You get a complete, immutable audit trail for compliance and auditing.

CQRS:

Commands change state on the write side (validate rules, append events).

Queries hit read models tailored for dashboards: “pending approvals for my team,” “spend by category last 90 days,” “top policy violators,” etc.

Scalability & resilience: Read projections can be optimized independently (e.g., PostgreSQL/Elastic). Payment processing can be handled via an outbox or queue without blocking the command path.

Rebuildability: If read models get corrupted or evolve, replay events to rebuild them. Snapshots keep rebuild time fast.
