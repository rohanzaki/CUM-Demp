# DEMP DCIM & Project Oversight Portal — Product Scope

## 0. One-Liner
A secure, web-based control room that gives DEMP a single source of truth for procurement → delivery → installation → handover projects and a live "digital twin" of the datacenter (racks, servers, cables, licenses), with accountability, approvals, and clear ownership at every step.

## 1. The Problem (As-Is)
- Government projects run across PCI → bids → RFP → award → multi-phase delivery, but tracking is scattered in emails and spreadsheets.
- Vendors sometimes under-deliver, skip documentation, or hide implementation details.
- Hardware arrives without proper labeling or license proof; cables aren’t marked; knowledge transfer is weak.
- When incidents happen (e.g., someone unplugs a server), there’s no quick, authoritative map to put things back.
- Admins lack a bird’s-eye view of portfolio status, risks, and bottlenecks; teams lack a single place to coordinate.
- **Impact:** Delays, rework, finger-pointing, lost knowledge, poor readiness, and fragile operations.

## 2. The Solution (To-Be)
A role-aware portal that covers the entire lifecycle: Procurement → Contracting → Delivery & GRN → Installation & Commissioning → UAT/Training → Handover/Warranty → Operations.

It unifies:
- **DCIM:** Racks, servers, patch panels, ports, cables, IPs, software assets, licenses, warranties.
- **Projects & Tasks:** Kanban, milestones, checklists, approvals, and evidence capture.
- **Procurement & Compliance:** PCI/RFP/award documents, BoM, partial shipments, acceptance notes, exceptions.
- **Knowledge Base:** Runbooks, SOPs, diagrams, vendor docs linked to real assets.
- **Visualization:** Rack elevations, port-to-port maps, and a node graph of connections.
- **Accountability:** Tamper-evident audit trail, ownership, SLAs, escalations, and readiness scores.

## 3. Personas & Permissions (RBAC Logic)
- **Admin (DEMP):** Full oversight across modules. Creates projects, assigns roles, approves steps, closes milestones, and signs acceptance. Manages users/roles and defines standards (labeling, naming, checklists).
- **Project Manager (DEMP):** End-to-end project control within assigned projects. Creates/edits milestones, tasks, checklists; records delivery; triggers approvals; views all assets tied to their projects; cannot manage global users.
- **Technician (DEMP):** Day-to-day operations—install, cable, label, verify. Creates/updates assets and cables; updates tasks; uploads evidence; runs checklists; cannot approve contracts or alter budgets; cannot manage user accounts.
- **Procurement Officer (DEMP):** Manages PCI, RFP, award docs, vendor profiles, BoMs, GRN/acceptance. Updates delivery status; flags discrepancies; requests clarifications; read access to related tasks/assets; no system-wide user management.
- **Vendor (External):** Limited access to awarded project(s) only. Uploads deliverables (documents, BoM, licenses, as-built diagrams), updates shipment status, responds to change requests, completes vendor checklists; no visibility beyond their own scope.
- **Viewer / Auditor (Read-only):** Full read of permitted projects and assets; no edits.

**General rule:** Users only see and act on records they own or are assigned to, plus anything Admin explicitly shares.

## 4. End-to-End Lifecycle & Workflow Logic
### A. Procurement & Contracting
1. **Create PCI:** Upload PCI doc(s) and define high-level requirements and budget envelopes.
2. **Vendor Bidding:** Track interested vendors, questions, submitted RFPs, and comparison notes.
3. **Award:** Select winner; capture award letter, contract, SoW, SLA, payment terms, and penalties.
4. **Compliance Matrix:** Side-by-side list of PCI requirements vs vendor commitments (auto “met/not met/partial” status per item).

### B. Project Kickoff
1. **Project Shell:** Name, objectives, budget, dates, vendor, PM, stakeholders.
2. **Milestones:** Define phases (e.g., Design, Procurement, Delivery, Installation, Commissioning, UAT, Handover).
3. **Acceptance Criteria:** Plain language per milestone outlining required evidence, tests, and documents.
4. **Checklists:** Pre-install site readiness, power/network readiness, safety, documentation completeness.

### C. Procurement Execution
1. **BoM:** Items, quantities, serial-tracking requirement, license requirement.
2. **Partial Shipments:** Record each shipment; attach delivery notes, invoices; mark discrepancies.
3. **GRN (Goods Received Note):** Accept/Reject; partial accept; reason codes; auto-create follow-up tasks for fixes.
4. **License Intake:** Record key/entitlement, expiry, owner, and vendor contact for renewals for any item needing a license.

### D. Installation & Commissioning
1. **Work Orders:** Tasks with step-by-step checklists and required evidence (photos of rack face, cable labels, port mapping screenshots).
2. **Labeling Standard:** Portal generates label IDs for racks, U-positions, patch panels, ports, and cable A-end/B-end; printable sheets; QR codes on assets linking to the asset page.
3. **Validation Rules:** Prevent placing servers in occupied U space; warn on power/cooling oversubscription; require cable endpoints to be compatible and available.
4. **Commissioning Tests:** Define pass/fail tests (e.g., link up, throughput sample, service reachability); capture results and sign-off.

### E. UAT & Training
1. **UAT Plan:** Define demo/test scope (e.g., OCR accuracy, ad detection, channel coverage); identify sign-off stakeholders; capture evidence.
2. **Training:** Record sessions, attendee list, slides/videos; attach runbooks; quick-reference cards for on-call staff.

### F. Handover, Warranty, and O&M
1. **Handover Package:** One-click “Project Dossier” (contract, as-builts, asset list, licenses, passwords escrow note, test results, SOPs).
2. **Warranty & SLA:** Record start/end dates; response and resolution targets; link to vendor contacts and escalation ladder.
3. **Renewals & Expiries:** License and warranty calendars; upcoming-expiry lineup with owner assignment.

## 5. Core Modules & Capabilities
1. **Authentication & Security**
   - Login with role-based views.
   - Least-privilege defaults.
   - Record-level visibility tied to project membership or explicit sharing.
   - Tamper-evident audit log of every change (who, what, when, before/after summary).
2. **Home Dashboard (Bird’s-Eye)**
   - Portfolio health: Projects by status, on-time vs late milestones, budget burn vs plan.
   - Risk & gaps: Overdue deliveries, missing licenses, unassigned tasks, failed tests.
   - Datacenter snapshot: Racks/servers in use, active connections, recent changes, open incidents.
   - Vendor scorecards: On-time %, documentation completeness, rework count, SLA adherence.
3. **Procurement & Contracts**
   - PCI/RFP/award document vault with version history.
   - Vendor profiles: Performance history, prior disputes, designated contacts.
   - BoM with shipment tracking, GRN, discrepancy handling, and acceptance.
   - Compliance matrix auto-updated by evidence submissions.
4. **Projects & Milestones**
   - Projects list with status, health score, and next required action.
   - Milestones with acceptance criteria and readiness bars tied to evidence/checklists.
   - Change requests (scope/time/cost) with justification and approval trail.
5. **Tasks & Kanban**
   - Kanban board (To Do, In Progress, In Review, Done).
   - Task attributes: Title, description, priority, assignee, due date, checklist, attachments, comments, @mentions.
   - “Definition of Done” enforced by required checklist items/evidence.
6. **DCIM — Assets & Cables**
   - Racks: Name, location/room/row, size (U), power budget.
   - Servers/Appliances: Assigned rack + U range, owner project, serials, links to licenses and runbooks.
   - Patch Panels & Ports: Port lists with labels; port status (free, used, reserved).
   - Cables: A-end/B-end, type, color, length, label IDs; validation prevents impossible connections; status (planned, installed, verified).
   - Software/Licenses: Product name, entitlement, key or entitlement ID, expiry, assigned asset(s), renewal owner.
   - IP/Service References: Human-readable notes to locate services without deep network tooling.
7. **Visualization**
   - Rack elevation: Front view at correct U heights; hover for details; conflict warnings.
   - Port-to-port map: Select a cable to see both endpoints and path.
   - Topology graph: Draggable nodes (servers, panels, switches, vendor black-box), labeled edges (cables/links), filter by project or room.
8. **Labeling & QR**
   - System generates human-friendly, unique label IDs for racks, U slots, panels, ports, cables.
   - Printable sheets (A4) and QR stickers.
   - Scanning a QR opens the matching asset in the portal (mobile-friendly).
9. **Knowledge Base**
   - SOPs, runbooks, “how to” pages, and diagrams.
   - Articles link to specific assets/projects.
   - Required reading for certain tasks or roles.
10. **Incidents & Change Management**
    - Incidents: Impact, timeline, root cause, corrective/preventive actions.
    - Change requests: Risk level, planned window, approvals, rollback plan, success verification.
    - Unplug guardrail: Change ticket must link to exact cable/port with restoration plan and pictures; post-work verification required.
11. **Inspections & Audits**
    - Scheduled audits with checklists (labels, cable strain relief, dust, licensing proof).
    - Findings create tasks; trend reports show improvement/backsliding.
12. **Reporting & Exports**
    - Project Dossier PDF for handovers/auditors.
    - License & warranty calendar for upcoming expiries (30/60/90 days).
    - Compliance vs PCI with status (Green/Amber/Red) and evidence links.
    - Vendor performance metrics (lead times, misses, documentation quality, rework).
    - Asset register export (CSV/PDF) by room/rack/vendor/project.
13. **Notifications & Reminders**
    - Due/overdue tasks, milestone readiness, license expiries, shipment delays, SLA breach warnings.
    - Mentions (@name) notify the mentioned user.
    - Weekly admin digest of risks and pending approvals.
14. **Data Onboarding**
    - Guided import from spreadsheets for racks, servers, ports, cables, and licenses.
    - Preview + validation (duplicates, impossible connections, missing fields) before commit.

## 6. Special Template: "Monitoring System" (DEMP Use Case)
- **Scope Slots:** Channels list, ingest method, OCR accuracy targets, ad-detection requirements, transcript retention policy.
- **Acceptance Evidence:** Live demo checklist, sampling tests, error handling demonstration, failover plan.
- **Runbooks:** Restarting pipelines, GPU diagnostics, escalation guidance.
- **Artifacts Required:** As-built diagrams, support contacts, admin credentials escrow note, training recordings.
- **Operational KPIs:** Uptime %, incident count, MTTD/MTTR, backlog of mislabeled segments.

## 7. Cross-Cutting Rules & Logic
- **Ownership:** Every project, asset, task, cable, license has an explicit owner (person/role). Nothing is ownerless.
- **Readiness Gates:** Milestones and tasks can only close when required evidence and checklists are complete.
- **Evidence-First Culture:** Photos, PDFs, test results, and sign-offs live in the portal; verbal claims don’t move status.
- **Single Version of Truth:** The portal is authoritative—if it isn’t logged, it didn’t happen.
- **Least Privilege:** People see only what they need; vendors never see other projects.
- **Auditability:** Every change is recorded with who/when and a human-readable summary.
- **Restoration-Friendly:** Labels + topology + photos must make it possible to restore a rack from scratch without guessing.

## 8. UX & Branding Notes
- Clean, calm, government-grade UI.
- Suggested palette: Dark green/black base with yellow accents for emphasis; ensure accessible contrasts.
- Mobile-friendly for technicians (photos, QR scan, quick checklists).
- Progressive disclosure keeps dashboards simple while surfacing details on demand.
- Plain language everywhere (“Who is doing what by when?”).

## 9. MVP vs Phase 2
- **MVP (must ship):**
  - Auth & roles (Admin, PM, Technician, Procurement, Vendor, Viewer).
  - Projects, milestones, tasks with checklists and evidence.
  - DCIM core: Racks, servers, panels/ports, cables with validations and rack elevation view.
  - Procurement basics: PCI/RFP/award vault, BoM, shipments, GRN, license intake.
  - Label generator + printable labels + QR scanning.
  - Knowledge base linking to assets.
  - Reports: Project Dossier, License Expiry, Compliance vs PCI.
  - Audit log and notifications.
- **Phase 2 (nice-to-have):**
  - Topology graph and floorplan maps.
  - Vendor scorecards and SLA dashboards.
  - Incident & change management with RCA library and trend analysis.
  - Automated readiness scores and risk predictions.
  - API hooks to ingest emails/calendar or monitoring alerts.

## 10. Success Metrics
- 100% of active projects have a current milestone plan with owners and dates.
- 100% of installed assets have labels and photos.
- ≥95% of cables mapped with A-end/B-end recorded.
- All licenses/warranties have an assigned renewal owner and an upcoming-expiry status.
- Time to resolve “mystery unplug” incidents reduced by >75%.
- Vendor documentation completeness >90% by first handover attempt.
- Auditor requests satisfied via single dossier export—no scavenger hunts.

## 11. Edge Cases & Safeguards
- **Partial/Incorrect Deliveries:** GRN records partial accept; portal auto-creates discrepancy tasks and pauses dependent milestones.
- **Scope Changes Mid-Project:** Formal change request; budget/time impact surfaced; no “silent” changes.
- **Staff Turnover:** Ownership reassignment workflow to prevent orphaned responsibilities.
- **Disputed Evidence:** Mark as “contested”; require counter-evidence or arbitration by Admin.
- **Sensitive Docs:** Mark as “restricted”; only named roles can view/download.

## 12. Implementation Order (Developer Hint)
1. Roles & visibility → Projects/Milestones/Tasks → Evidence & checklists.
2. DCIM base (racks/servers/ports/cables) with rack elevation and validations.
3. Procurement (PCI/RFP/award, BoM, shipments, GRN, licenses).
4. Labels/QR + mobile evidence capture.
5. Reports (Dossier, Expiries, Compliance).
6. Knowledge base; then topology map and incident/change workflows.
