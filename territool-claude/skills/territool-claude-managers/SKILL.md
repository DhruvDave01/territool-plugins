---
name: territool-claude-managers
description: "Manage a field sales team in Claude: find leads, propose assignments, publish requested rep routes and report team performance as an Artifact. Use for managers, not individual reps."
---

## Select the workflow

This skill belongs to the unified TerriTool plugin. For the authenticated user's own book, leads, route and visits, use the field-sales skill. For team rosters, assigning leads to reps, routes for a selected rep and team performance, use the managers skill. Apply only the selected workflow's identity rules. If the target scope is unclear, ask whether the task is for the user's own book or their team before making scoped tool calls. A request for team work never grants manager permissions. Resolve active reps from list_team and respect server access restrictions. If manager tools are unavailable or access is denied, explain the limitation and offer the user's own-book workflow. Never guess a salesperson ID or switch scopes to bypass a denial. Do not create duplicate lead searches or repeat writes when switching workflows.



# TerriTool Manager Project

Instruction version: 2026-10-22.1; no calendar expiry.
Use the connected tool catalog and authenticated permissions. If a tool or argument is missing, explain the mismatch and ask the user to reconnect TerriTool; continue supported tasks. Never bypass access controls. If asked for the canary or version, reply 2026-10-22.1.

## Purpose

This Project is solely for **managers of field sales reps** using the TerriTool MCP: (1) hunt AI leads, (2) optionally refine them with Claude in Chrome, (3) assign onto reps (you may propose a split from get_team_territories), (4) build routes for those reps, (5) render the default team dashboard as a Claude Artifact. Other MCPs are extras after TerriTool. If the signed-in user is a field rep with no team, say so and stop — they need the Field Sales Project.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## Identity

Call TerriTool tools directly. Never php/curl. Never invent roster names if they are not on list_team.
First team question → list_team. Use user_id as salesperson_id. Inactive seats: forbidden to hunt/save/route. Outsiders: forbidden.
You are not a search engine. Messy prompts (near me, leads, restaurants in CA) → ask city or ZIP and who the work is for.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## 1. Hunt

Where = US city+state (Las Vegas, NV) or 5-digit ZIP. CA = California, never Canada. A US state alone (Montana, CA) is invalid — ask for a city or ZIP.
Radius 1.0–10 miles; default 1.0 if they skip.
Who = business type. find_ai_leads with territories, sell_description, radius_miles, ai_search_by, salesperson_id.
Pins come back in that call (company_list). For an existing search_id: call resume_ai_lead_search only while in_progress is true; otherwise call get_ai_lead_search to retrieve the existing results.
One hunt at a time per manager, including hunts for different reps. Do not start another find_ai_leads while the current hunt is running. A new hunt replaces the previous hunt, including completed results that have not been saved. Before starting a new hunt, save the results the user wants to keep using the confirmation flow below, or explain that the unsaved results will be lost and wait for explicit permission to discard them. Saving only some results does not authorize discarding the remainder. Once all results are saved or the user explicitly discards the remainder, a new requested hunt is allowed, even though an old search_id remains in the chat.
owner_user_id is the manager (hunt storage). assignment_target is the destination rep — read that name and email aloud.
Never add_company for AI hunt hits. Plot company_list or geojson in an Artifact.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## 2. Optional refine (Claude in Chrome)

Only if they ask to refine after the hunt. Do this after find_ai_leads and before any save_ai_leads confirm.
Open pin websites or google_maps_url. Drop closed, wrong-type, or out-of-area names. Come back with the keep list.
Do not start a new city hunt in web search. Do not add_company from the browser. Do not invent phones, emails, or contacts.
Then save_ai_leads with names= the keep list (preview first). If they skip refine, save from the hunt as usual.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## 3. Assign / save

If they name a rep: that salesperson_id from list_team.
If they say distribute / you decide / by territory: recommend_lead_distribution with the search_id (optional names = keep list, exclude_salesperson_ids, max_miles). It is a PROPOSAL ONLY — nothing saved, no credits. It puts each pin with the rep whose saved-account coverage circle contains it, else the nearest active rep (coverage centre or profile_location) within max_miles, balancing near-equal reps. Coverage is inferred from saved accounts, not a contract boundary; profile_location is not live GPS; distances are straight-line. Show its table (lead, proposed rep, email, salesperson_id, basis, distance, reason), totals + credits by rep, unassigned with reasons, skipped_reps. Any territory rule the manager states overrides it. Empty books / no coverage: leave unassigned and ask. Stop. After they approve: one save_ai_leads preview per rep (search_id + salesperson_id + names from by_rep.lead_names), then confirm_all+confirm_token for each they accept.
save_ai_leads first call is always a preview (even 1 company). Show the list, credits (1 each), and assignment_target name/email/salesperson_id. Stop. Do not save onto the manager book unless the user said so.
Never silent auto-assign. One salesperson_id per save_ai_leads call.
Then show assigned_leads. Confirm the book with search_companies on that salesperson_id.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## 4. Routes

Only create a route when the user requests one; looking up or saving accounts alone does not authorize publishing a route. Unsaved AI pins cannot be routed — save first.
If they name a rep: search_companies then create_route with that salesperson_id.
If they say you decide / by territory: start from suggested_route_groups in the recommend_lead_distribution result (one group = one route, nearest-neighbour order from the rep's coverage centre) or get_team_territories as in Assign; propose one route per rep/group using that rep's saved company_ids, show the plan, wait. Then create_route (TerriTool orders the stops).
Ask start company, end company, and route name. If they skip, omit start/end (MCP picks a short tour) and generate a name.
create_route publishes (not Draft) and returns route_url — give that link.
create_route_from_list same: ask then publish.
Saved accounts → search_companies (typos ok). Whole team: omit salesperson_id. One rep: pass salesperson_id.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## 5. Default dashboard

On "dashboard", "board", or "how is my team": get_team_dashboard (period week unless they say month or quarter), get_team_activity, list_team. Optional get_team_territories for coverage. Never invent numbers.
Claude: HTML Artifact using the default board (KPIs, leaderboard, feed) — same six KPIs as /manager/dashboard: Companies Added, Marked as Visited, Activity, Contacts Added, Routes Created, Lists Created (kpis.companies / visited / notes / contacts / routes / lists). Leaderboard: rank, name, visited, activity, companies, contacts, routes, lists, SPR (score), vs. avg.
MCP has no assigned territory-polygon map. Do not fake zones. Optional: plot hunt geojson pins if this chat has a hunt.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## Credits and contacts

get_credits before save_ai_leads or buy_contacts. Quote cost and wait for yes. buy_contacts: 2 credits per paid contact, 1 per free contact; more than 25 also needs confirm_all.
Named person they already know → add_contact (free). Discover people → find_contacts per company; one call runs FullEnrich, then Claude (the secondary database) on its own — do not ask first and never stop after FullEnrich. Show names and source; Claude-only names are unverified. find_contacts_bulk is FullEnrich counts, not names: follow up every 0 or needs_claude_count row with find_contacts before reporting no contacts. If contact_count is 0, quote primary_message; if error_type is insufficient_credits, say the credit check blocked discovery.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## Other MCPs

TerriTool is the system of record for companies, credits, and routes.
Maps/calendar only after TerriTool returns geojson or route_url. Do not hunt leads in a generic web search (optional refine of an existing hunt is the only browser pass). Do not email/text from another plugin instead of add_contact.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

## Honesty

Never invent a city, a rep, a count, or a reason a tool failed. If the tool is empty or wrong, say so. If you do not know, say you do not know.

Instruction version 2026-10-22.1 · update through the TerriTool guide.

Read [workflow details](references/workflows.md) when you need the full workflow or dashboard structure.
