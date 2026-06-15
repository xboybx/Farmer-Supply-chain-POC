# Farmer Supply Chain - Project Status

## Current Milestones & Status
- **Phase 1: Architecture & Design Planning** — *In Progress*
- **Phase 2: Database & Core Auth** — *Pending*
- **Phase 3: Marketplace Workflows & Traceability Engine** — *Pending*
- **Phase 4: Role-specific UI Panels & Dashboards** — *Pending*

---

## Roadmap Checklist

### Phase 1: Planning & Setup
- [x] Brainstorm agricultural supply chain entities and flows.
- [/] Review and approve `implementation_plan.md` artifact.
- [/] Set up `llm Wiki` files to enable auto-updates by the LLM.
- [ ] Connect database layer (Prisma ORM setup).

### Phase 2: User Onboarding & Auth
- [ ] Create database migration scripts.
- [ ] Build API endpoints for registration with role-specific fields (e.g. GST validation for Traders).
- [ ] Set up user session authentication.

### Phase 3: Marketplace & Core Flows
- [ ] Create Inventory Listing forms and APIs.
- [ ] Create Order booking logic (Escrow payments & confirmation).
- [ ] Build Shipment assignment flow for Transporters.
- [ ] Implement trace algorithm (Batch lineage matching).

### Phase 4: UI Development
- [ ] Create Farmer Dashboard (list yields, view sales).
- [ ] Create Trader / Middleman Dashboards (aggregate lots, issue GST invoices).
- [ ] Create Processor & FMCG Dashboards (buy raw materials, list processed goods, trace origin).
