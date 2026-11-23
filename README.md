# Business plugins: install guide

How to get the same business plugins Badr uses (`small-business`, `sales`, `finance`, `legal`, `marketing`, `operations`, `product-management`, `productivity`, `enterprise-search`, `data`) on your own machine, in Claude or in Antigravity.

These plugins are published by Anthropic's marketplace, not by Badr. This repo does not copy them: you install each one from the marketplace, so you always get the current version.

## 1. Claude (claude.ai, Claude desktop, Cowork)

1. Open **Customize** in the left sidebar, then the **Plugins** tab. In Cowork, open the Cowork tab first.
2. Click **Browse plugins** (or **Discover**).
3. Install each plugin from the list above.

Plugins you add on the web or desktop are saved to your account, so they also show up in chat, Cowork and Claude Code.

Use a skill by typing `/` and picking it, or by running `/plugin-name:skill`, for example `/small-business:business-pulse`.

Each person installs for their own account. Connect your own tools (QuickBooks, Gmail, HubSpot and so on) when a skill asks. Nobody else's data is shared.

## 2. Claude Code (terminal)

```bash
claude plugin marketplace add anthropics/knowledge-work-plugins
claude plugin install small-business@knowledge-work-plugins
claude plugin install sales@knowledge-work-plugins
claude plugin install finance@knowledge-work-plugins
```

Plugins installed from the command line stay on that machine and are not added to your account.

## 3. Antigravity (Google)

Antigravity runs the same `SKILL.md` skill folders, but it does not use Claude's plugin system. Two ways:

**A. Copy the skill folders (recommended, works for sure)**

```bash
git clone https://github.com/anthropics/knowledge-work-plugins.git
# global, all projects
mkdir -p ~/.gemini/config/skills
cp -r knowledge-work-plugins/small-business/skills/* ~/.gemini/config/skills/
# or one project only
mkdir -p .agents/skills
cp -r knowledge-work-plugins/small-business/skills/* .agents/skills/
```

Repeat with `sales`, `finance` and the others you want. If a plugin has no `skills/` folder, check its layout in the repo first.

Use them by typing `/<skill-name>` (for example `/business-pulse`), or just describe the task and the agent picks the skill.

**B. Plugin command (untested)**

```bash
agy plugin install https://github.com/anthropics/knowledge-work-plugins
```

Antigravity documents installing a skill bundle from a GitHub URL, but I could not confirm that it accepts Claude-style plugins. If it fails, use option A.

**Limits in Antigravity**
- The `plugin:skill` names (`/small-business:business-pulse`) are Claude's. In Antigravity the name is just `/business-pulse`.
- Connectors (QuickBooks, Gmail, HubSpot…) are set up separately through MCP servers; copying skills does not connect them.
- Skills that write to the user's accounts or move money always ask for approval first. Keep that on.

## 4. What the small-business plugin contains (44 skills)

| Area | Skills |
|---|---|
| Daily / weekly pulse | `business-pulse`, `monday-brief`, `growth-pulse`, `marketing-monday`, `report-builder`, `report-pack` |
| Cash and books | `cash-flow-snapshot`, `invoice-chase`, `ap-processor`, `pay-the-bills`, `month-end-prep`, `close-month`, `tax-prep`, `tax-season-organizer` |
| Payroll and hiring | `payroll-prep`, `plan-payroll`, `job-post-builder`, `hiring-screener` |
| Sales and leads | `lead-finder`, `lead-triage`, `call-list`, `speed-to-lead`, `outreach-composer`, `grow-pipeline`, `crm-autopilot`, `proposal-builder`, `reactivate` |
| Marketing | `content-strategy`, `social-content-engine`, `canva-creator`, `ad-manager`, `seo-ai-visibility`, `review-reputation`, `brand-style` |
| Operations | `inventory-planner`, `restock`, `inbox-manager`, `ticket-deflector`, `contract-review`, `grant-rfp-writer` |
| Setup | `smb-onboard`, `smb-router`, `build-agent`, `build-connector` |

Start with `smb-onboard`: it connects two tools, runs one first task and sets a weekly routine.

## 5. Other plugins in this stack

| Plugin | Good for |
|---|---|
| `sales` | Call prep, account research, deal and pipeline review, forecast |
| `finance` | Journal entries, reconciliation, financial statements, variance analysis |
| `legal` | Contract review, NDA triage, compliance checks |
| `marketing` | Campaign plans, content drafts, email sequences, performance reports |
| `operations` | Process docs, runbooks, vendor reviews, status reports |
| `product-management` | Specs, roadmaps, research synthesis, stakeholder updates |
| `productivity` | Task list and context memory |
| `enterprise-search` | One search across email, chat and docs |
| `data` | SQL, exploration, dashboards |

## Updating

Claude: Customize → Plugins updates from the marketplace. Antigravity: `git pull` in the cloned repo and copy the folders again.
