# Newcomer Guide + Mobile Setup Playbook

## 1) Objective
Get a new contributor productive in **under 60 minutes** and prevent accidental branch deletion by setting a safe GitHub ruleset from mobile.

---

## 2) Step-by-step execution

### A) Understand what this repo contains (fast)
This repository is a **logic-first RCM automation starter** with two production-relevant assets:

1. `base_camp_schema.sql` → intake + eligibility data model.
2. `peak_denial_engine.json` → denial code response playbooks.

There is no API/UI service yet; this is currently a rules-and-data foundation.

### B) Learn the architecture in the right order

#### Step 1 — SQL data foundation
Read `base_camp_schema.sql` in this sequence:
- `Patients`
- `InsuranceProviders`
- `EligibilityAudits`
- `Intake_Leakage_Report` view

Why this order works:
- It follows relationship flow from patient intake → payer mapping → eligibility outcomes → leakage reporting.

#### Step 2 — Denial automation logic
Read `peak_denial_engine.json` and map each code to operations:
- CO-18 → duplicate claim recovery pathway
- CO-16 → missing info remediation pathway
- PR-1 → patient responsibility pathway

#### Step 3 — Translate to workflow
Use this trigger chain:
1. Intake event stored in SQL.
2. Eligibility issue flagged by view.
3. Denial event matched to JSON rule.
4. Action task generated (work queue/ticket).
5. Outcome logged for KPI reporting.

### C) Addressing your screenshot workflow (GitHub mobile ruleset)
Your screenshots show you are configuring **Rulesets** on mobile. Use this exact minimal configuration to protect key branches quickly.

#### Step 1 — Ruleset name
Use one of these names:
- `protect-main-v1`
- `protect-production-v1`

#### Step 2 — Enforcement status
- Start with **Active** if you are ready now.
- If testing first, set **Disabled**, save, then switch to Active after validation.

#### Step 3 — Target branches
Tap **Add target** and set one pattern:
- `main`

Optional second ruleset for release branches:
- `release/*`

#### Step 4 — Turn on these branch rules (minimum safe profile)
Enable:
- ✅ Restrict deletions
- ✅ Require pull request before merging
- ✅ Require approvals (1 minimum)
- ✅ Require status checks to pass (if CI exists)

Leave off for now (to avoid friction on early-stage repos):
- ❌ Require signed commits
- ❌ Require deployments to succeed

#### Step 5 — Bypass list
Keep bypass list empty unless strictly needed.
If needed, add only owner/admin account.

#### Step 6 — Save + test
1. Save ruleset.
2. Open a test branch and verify you can still create PRs.
3. Confirm direct delete/push-to-main is blocked.

---

## 3) Tools (free only)
- GitHub mobile web/app (rulesets + PR workflow)
- MySQL Community or PostgreSQL (local/free tier)
- Python 3 (rule-runner prototype)
- GitHub Actions free tier (basic checks)
- Metabase OSS (optional KPI dashboard)

---

## 4) Copy-paste output

### A) Branch protection profile (copy into your implementation checklist)
```md
Ruleset Name: protect-main-v1
Enforcement: Active
Target Branches: main
Rules:
- Restrict deletions: ON
- Require pull request: ON
- Required approvals: 1
- Require status checks: ON (if CI exists)
- Require signed commits: OFF
- Require deployments: OFF
Bypass list: none
```

### B) 60-minute onboarding checklist
```md
- [ ] Read README.md for mission + modules
- [ ] Load base_camp_schema.sql into local DB
- [ ] Seed sample Patients/InsuranceProviders/EligibilityAudits rows
- [ ] Run Intake_Leakage_Report and verify non-Verified records only
- [ ] Parse peak_denial_engine.json and map urgency -> queue priority
- [ ] Create one pseudo-automation flow: event -> rule -> task -> KPI
- [ ] Configure protect-main-v1 ruleset on GitHub
```

### C) Next build sprint (income-generating focus)
```md
Sprint Goal: reduce denial rework time and improve collection speed
1) Build Python worker to load JSON rules
2) Query new eligibility/denial events every 15 minutes
3) Auto-create action tasks by urgency
4) Track 24-hour interception KPI
5) Publish weekly savings report (hours recovered + $ recovered)
```

---

## 5) Expected result
- New contributors understand architecture and system boundaries quickly.
- Main branch is protected against accidental deletion/unsafe updates.
- Team has a direct path from static logic files to scalable automation with measurable revenue-cycle impact.
