# TerriTool Field sales — Project knowledge (Claude)

Upload this file into the Field Sales Claude Project (**Context → + → Upload from device**). It is knowledge for one rep’s working day. It is not Manager instructions. Solely claude.ai or Claude Desktop; not Claude Code.

Use the connected TerriTool tools only. Never php/curl. Never salesperson_id. Never list_team.

## Today’s loop

1. Saved book → `search_companies` / `view_company`. All routes → `view_routes`; all lists → `view_lists`.
2. New leads → `find_ai_leads` (US city+state or ZIP). Hunting is free. Redisplay a finished hunt → `get_ai_lead_search`.
3. Save → `get_credits`, then `save_ai_leads` preview, wait for yes, then `confirm_all` + `confirm_token`. One credit per lead.
4. Route only if they asked → `create_route` or `create_route_from_list` (both publish). Share `route_url`.
5. On the street → `get_active_route`, `next_waypoint`, `mark_visited`, `add_activity`, `add_note`.
6. People they already know → `add_contact` (free). Discover → `find_contacts` per company. One call runs FullEnrich, then Claude (the secondary database) on its own — never ask first, never stop after FullEnrich. `find_contacts_bulk` is FullEnrich counts only; follow up every 0 or `needs_claude_count` row with `find_contacts` before saying there are no contacts. Then `buy_contacts` only after quoting credits.

Walked into a new place → `add_company`, not `save_ai_leads`.

Optional website checks: Claude in Chrome, only if it is connected. Skip it if the TerriTool data is enough.

## Do not

- Assign work to a teammate.
- Hunt “near me” without a city or ZIP.
- Start a second hunt while the first unsaved hunt is still needed.
- Invent phones, emails, or a reason a tool failed.
