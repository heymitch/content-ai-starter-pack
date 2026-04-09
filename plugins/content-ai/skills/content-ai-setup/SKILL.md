---
name: content-ai-setup
description: Set up your Content AI system — creates a Notion content calendar database and connects it to your workspace. Say "set up my content system", "content setup", or "get started with content".
user-invocable: true
---

# Content AI Setup

Creates your Notion content calendar and wires it into your workspace. Every content skill writes here automatically after setup.

## Step 1: Check Existing Config

Read `.coworker/index.md` (if it exists). Look for an existing content calendar URL or content section.

- If a Notion content calendar URL already exists: tell the user it's already set up, show the URL, and stop.
- If not: proceed to Step 2.

## Step 2: Create the Notion Content Calendar

Use the Notion MCP to create a new database in the user's Notion workspace.

**Database name:** `Content Calendar`

**Schema:**

| Property | Type | Options |
|----------|------|---------|
| Name | title | — |
| Platform | select | Substack, LinkedIn, Twitter, Email, YouTube |
| Status | select | Draft, Ready, Published, Archived |
| Publish Date/Time | date | — |
| Suggested Edits | text | — |

Create the database as an inline database on a new page called "Content Calendar" in the user's workspace. If the user specifies a parent page, create it there.

## Step 3: Save to Workspace Index

Add a Content section to `.coworker/index.md`:

```markdown
## Content
- Content Calendar: [Notion URL from Step 2]
- All content skills write here automatically
- Title → Name property, body → page content
- Set Platform and Status when creating entries
```

If `.coworker/index.md` doesn't exist, create it with a header and this section.

## Step 4: Confirm

Tell the user:

```
Content calendar created: [URL]

Every content skill now writes here:
- LinkedIn AI → Platform: LinkedIn
- Newsletter Writer → Platform: Substack
- Social Repurposer → creates one entry per platform
- Email Sequence Writer → Platform: Email

All entries start as "Draft". Open your calendar in Notion to review and publish.
```

## Rules

- Do NOT re-ask for niche, pillars, or voice config if `.coworker/index.md` already has this info.
- Do NOT generate a local markdown calendar. Everything goes to Notion.
- The database must be blank — no sample entries.
- If Notion MCP is not connected, tell the user: "Connect Notion in Cowork settings first, then run this again."
