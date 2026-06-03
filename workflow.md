# Calma Studio — Automation Workflow

This document describes the end-to-end automation workflow that powers 
Calma Studio's content system.

---

## How it works — overview
[Notion Input] → [Zapier] → [Claude API] → [Zapier] → [Social Media]
→ [Notion Calendar]
---

## Step 1 — Content input (Notion)

The team fills in a simple Notion database row with:

| Field | Description | Example |
|-------|-------------|---------|
| Topic | The wellness theme | "Work anxiety" |
| Platform | Where to publish | Instagram, LinkedIn, Facebook |
| Language | Target language | ES, PT, EN |
| Publish date | Scheduled date | 2026-06-10 |
| Status | Current state | Draft |

When Status changes to "Ready" → Zapier triggers automatically.

---

## Step 2 — Zapier trigger

**Trigger:** New row in Notion database with Status = "Ready"

**Zapier reads:**
- Topic
- Platform
- Language
- Publish date

---

## Step 3 — Claude generates content

**Zapier action:** Claude API call

Zapier selects the correct prompt template based on Platform + Language 
and sends it to Claude with the Topic filled in automatically.

**Example:**
- Platform: Instagram · Language: ES → uses PROMPT 1
- Platform: LinkedIn · Language: EN → uses PROMPT 4
- Platform: Facebook · Language: ES → uses PROMPT 6

---

## Step 4 — Content goes back to Notion

Claude's response is written back to the Notion row:
- Generated caption saved in "Content" field
- Status updated to "Generated — pending review"
- Team reviews and approves in Notion

---

## Step 5 — Publishing (after approval)

When Status changes to "Approved" → Zapier triggers again:

| Platform | Zapier action |
|----------|---------------|
| Instagram | Publishes via Instagram Graph API |
| LinkedIn | Publishes via LinkedIn API |
| Facebook | Publishes via Facebook Pages API |

---

## Step 6 — Editorial calendar update

After publishing, Notion row is automatically updated:
- Status → "Published"
- Published date logged
- Platform and language recorded

This builds a full content history automatically.

---

## Time saved

| Task | Before | After |
|------|--------|-------|
| Writing captions | 3.5 hrs/week | 20 min review |
| LinkedIn posts | 2 hrs/week | 10 min review |
| Facebook posts | 2 hrs/week | 10 min review |
| Translation | 2 hrs/week | Automatic |
| Calendar update | 1.5 hrs/week | Automatic |
| **Total** | **12 hrs/week** | **40 min/week** |