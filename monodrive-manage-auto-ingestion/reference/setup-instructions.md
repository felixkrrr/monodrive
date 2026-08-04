# Setup Instructions

Read this file only when the journey requires a Monodrive Provider Connection, Raw Source inspection, or an Ingestion Automation.

Use Monodrive MCP tools for this workflow. Keep tool names and internal identifiers out of normal user reports.

## Connect and collect

1. Call `providers_list`.
2. Select the Provider named by the user.
3. Call `providers_get` with its Provider key.
4. Call `provider_connections_list`.
5. If no active Connection exists, call `provider_connections_create`, give the user its `setupUrl`, and wait for browser authorization.
6. Call `provider_connections_list` again and select the active Connection.
7. Call `raw_sources_refresh` when collection has not started automatically.
8. Poll `provider_connections_get` at a measured cadence until its latest collection Run is terminal.
9. Call `raw_sources_list`, then inspect representative sources with `raw_sources_get` and `raw_sources_evidence_get`.

Use Provider credentials only through the Provider Connection. Report actionable collection errors as returned.

**Gate:** The Connection is active, collection is terminal, and representative evidence is available.

## Understand the Brain

Call `schema_get`. Call `schema_type_get` for each relevant Page Type. Use `query` and `pages_get` to inspect relevant Pages.

**Gate:** The active Schema, relevant Page Guidance, and possible destination Pages are understood.

## Prepare the Automation

Read and apply [the Automation instruction rules](automation-instructions.md).

Create one narrow filter and one ingestion instruction. Call `ingestion_automations_create`; the new Automation remains paused.

**Gate:** The paused Automation has reviewed instructions that fit the active Schema.

## Preview and revise

1. Select one representative Raw Source Version.
2. Call `ingestion_runs_start` with `mode: preview`.
3. Poll `ingestion_runs_get` until the Run is terminal.
4. Inspect the filter decision, evidence limits, and proposed Page changes.
5. State that the preview made no Brain changes.
6. When the result needs revision, call `ingestion_automations_update` and preview the new immutable revision.

Treat `failed` and `filtered` Runs as terminal without apply. Treat a proposal that contains only `no_op` mutations as no Brain change. Preserve error codes, write effects, retry guidance, and bounded context when the user needs to resolve an error.

**Gate:** A terminal preview matches the selected outcome and the user explicitly approves it.

## Apply and verify

1. Call `ingestion_runs_apply` with the approved Preview Run ID.
2. Poll `ingestion_runs_get` until the apply Run is terminal.
3. Confirm that its state is `applied`.
4. Call `pages_get` for every created or updated Page.
5. Report only changes that the stored Pages confirm.

**Gate:** The exact approved preview is applied, and every reported Page change is verified.

## Process selected past sources

For each selected past source, run a new preview. Apply it only after the user approves that preview.

**Gate:** Each requested past source has a verified result or a reported terminal exclusion or failure.

## Activate and monitor

Call `ingestion_automations_set_state` with `active` only after an approved apply succeeds and the user approves prospective ingestion.

Explain that activation is prospective. Previously collected sources are not processed automatically.

Use `ingestion_runs_list` and `ingestion_runs_get` to verify recurring Runs. When an Automation needs attention, keep it paused until the error is repaired, then preview again before activation.

Use `ingestion_runs_replay` only for a one-time audited override of an excluded Run and only when the user supplies the reason.

**Gate:** The requested Automation state is confirmed, and the user understands how future and past sources are handled.