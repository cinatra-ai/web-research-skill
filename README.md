# Cinatra Web Research Skill

The research methodology behind Cinatra's web-research step: given a batch of rows and a plain-language research goal, it verifies and enriches every row from the live web, writes down what it checked, and returns one strict JSON envelope instead of prose. It is the knowledge half of `@cinatra-ai/web-research-agent`, packaged as its own skill so any extension that declares a dependency on it gets the same discipline.

**Install:** Install `@cinatra-ai/web-research-skill` in your Cinatra instance. `@cinatra-ai/web-research-agent` installs it automatically as a declared dependency.

**Usage:** The skill is delivered into a run by the extension that depends on it — you do not invoke it directly. It expects `rows` (1–20 objects), a `prompt`, optional `sources` (up to 10), and an optional `outputSchema`.

**Configuration:** None. The skill carries no credentials and reads no settings; the host supplies the `web_search` tool.

**Development:** Clone the repository and run `node extension-kind-gate.mjs --package-root .` to validate the manifest. The bundle lives in `skills/web-research/` — a `SKILL.md` router plus one-hop reference files.

**Troubleshooting:** If a run returns an `input_bounds` failure, the caller sent more than 20 rows or more than 10 sources — chunk upstream. If rows come back with no `researchNotes`, the delivering extension is not mounting the bundle.

## Works with

- Cinatra web-research agent
- Any extension declaring a skill dependency on this package

## Capabilities

- Verify and enrich a caller-supplied batch of rows against live web sources
- Record every URL it consulted, including the ones that were unreachable
- Keep one output slot per input row, even when a row fails
- Enforce hard input bounds and return an early-error envelope instead of guessing
- Emit a strict JSON envelope with no surrounding prose
