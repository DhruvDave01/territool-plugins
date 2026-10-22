# TerriTool Field sales — Project knowledge (ChatGPT)

Upload this file into the Field Sales ChatGPT Project (**Add files**). It is knowledge for one rep’s working day. It is not Manager instructions.

Use connected TerriTool tools only. Never php/curl. Never salesperson_id. Never list_team.

## Today’s loop

1. Saved book → `search_companies` / `view_company`.
2. New leads → `find_ai_leads` (US city+state or ZIP). Hunting is free.
3. Save → `get_credits`, then `save_ai_leads` preview, wait for yes, then `confirm_all` + `confirm_token` with the preview’s `search_id`, `limit`, `names` and `min_rating` unchanged. One credit per lead. `confirm_held` → retry the identical call after `retry_after_seconds`. `confirm_token_mismatch` → nothing saved; confirm with `pending_confirm_token` and the preview’s filters, or preview again.
4. Route only if they asked → `create_route` (publishes). Share `route_url`. Keep a route to 15 stops or fewer unless asked; one call per route, and check `view_routes` before retrying a timed-out create.
5. On the street → `next_waypoint`, `mark_visited`, `add_activity`, `add_note`.
6. People they already know → `add_contact` (free). A plain “contacts” request → `search_companies`, then `find_contacts` for each selected company. Automatically complete the primary and secondary discovery chain without asking permission to check another source. Bulk counts are not names or final empty results: follow zero counts or secondary-follow-up flags with `find_contacts`; fetch names with that tool even for positive counts. No website does not mean no contacts. Show existing contacts when returned; report errors and credit blocks as incomplete searches. Only report no contacts after a successful completed lookup returns no discovered or existing contacts. Then `buy_contacts` only after quoting credits and receiving confirmation.

Walked-into a new place → `add_company`, not `save_ai_leads`.

## Do not

- Assign work to a teammate.
- Hunt “near me” without a city or ZIP.
- Start a second hunt while the first unsaved hunt is still needed.
- Invent phones, emails, or a reason a tool failed. An internal error carries a `reason`; `server_misconfigured` means credit writes are blocked until the admin runs the named migration.

Contact redemption: use discovery_id and selected contact_ids from find_contacts. Call buy_contacts first for a preview; show names and exact credit cost and stop. After agreement, repeat the same selection with confirm_all=true, confirm_token and a new idempotency_key. Poll get_contact_purchase_status(job_id); report success only when done=true and result.success=true. Never pass raw provider contact objects or redemption strings.

Workflow boundaries: stop after the requested task is complete. Saved-account searches only show results; create lists or routes only when requested. The full hunt → preview/confirm save → verify saved companies → create route → route_url sequence applies only when all those actions were requested. Reuse route and list preferences already provided. Show contact names and sources, flag mismatched or uncertain candidates, and do not present them as verified decision-makers or recommend them for redemption. A redemption preview is not approval. Execute only after explicit approval of selected contacts and exact credit cost. Use a new idempotency_key for the confirmed execution, different from any preview key; reuse that execution key and identical arguments on retries. Poll get_contact_purchase_status(job_id) after queueing.
