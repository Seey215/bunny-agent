# Verification and remaining acceptance

Date: 2026-10-16
Baseline: main@38c228c, v0.9.62
Status: 30 of 31 tasks complete. Task 7.2 remains unchecked.

## Scoped checks

- 44 affected test files passed, 536 tests total. Coverage includes manager
  contracts and CLI construction, SDK stream/generate/UIMessage handling,
  request isolation and peer compatibility, Pi marker/native/session/stream
  handling, provider normalization, harness dispatch, and Codex adaptation.
- Strict scoped SDK and Pi TypeScript checks passed. Manager compilation and
  SDK backend/contracts/React builds with declarations passed.
- Published-condition Node contract imports, TypeScript consumer imports,
  and the browser contract bundle passed. The browser bundle contains no
  Node hashing or orchestration imports.
- The compiled SDK root accepted a supported peer metadata fixture and
  retained acknowledgement/text metadata through a sandbox-adapter fixture.
  It rejected an older peer metadata fixture before sandbox attachment.
  These fixtures exercise package resolution and ES2022 output, not AI SDK
  execution. Separate unit regressions bundle the guard and run it in a
  fresh Node process for both peer versions.
- Seven documentation/design JSON examples and the illustrative handoff
  fixture passed contract validation. The handoff projection exactly matches
  `projectUIMessageOutputText()` from the built public SDK contracts entry;
  URL identities and the Unicode `[4,7)` example are verified.
- Scoped Biome checks and `git diff --check` passed.

Checks used workspace source aliases and isolated dependencies matching the
manifest's Pi 1.2.0 versions. Fresh Node child processes received matching
external dependency resolution. Installed library source was not patched;
verification configuration and logs are not release files.

## Actual model integration

All 10 scenarios passed through an actual `gpt-5.6-sol` model and native Pi,
using controlled Tavily HTTP responses. The matrix was rerun after the
final provider/parser and compiled-peer-guard repairs.

| Transport | Success | Empty | HTTP 429 | HTTP 401 | Legacy |
| --- | --- | --- | --- | --- | --- |
| Local daemon coding-run | Pass | Pass | Pass | Pass | Pass |
| Runner CLI fallback | Pass | Pass | Pass | Pass | Pass |

The chain includes SDK `streamText().toUIMessageStream({sendSources:true})`
and `readUIMessageStream()` on actual `ai@6.0.264`. Each successful transport
produced three model-authored citations. Every source binding matched its
executed search results, each code-point range covered its exact emitted
marker, and source events were unique. Empty and failed searches created no
citations. Failure envelopes survived in final tool-part
`resultProviderMetadata["bunny-agent"].search_result`; no error `output`
field is assumed. Legacy requests retained their original search format.

## Independent review repairs

Independent review reproduced and repaired nested Markdown code-fence
rewrites, harness authentication failures masked by fallback, and malformed
provider payloads misrepresented as confirmed empty results. Provider
conformance tests now distinguish explicit empty arrays from missing lists
and discarded rows, preserve legacy behavior, and compare equivalent Pi
and harness canonical results. V1 model-visible results contain validated
sources only. Container-prefix processing is bounded and retains later
text literally with partial diagnostics on overflow.

Publication review found that ES2022 bundling removed JSON import options
from the initial peer-version check. The backend now resolves peer JSON
lazily with Node `createRequire`; compiled-package tests cover both supported
and unsupported peers. V1 requires stable `ai >=6.0.264 <7.0.0`; legacy
retains `^6.0.0`. Packaged React hooks use `@ai-sdk/react ^3.0.267`.

## Remaining gates

Task 7.2 requires a **new runtime-supplied Tavily credential** for a fresh
real provider/model/daemon/SDK citation run. Earlier real Tavily source-card
evidence does not satisfy this task, and its discarded credential is not
reused. Controlled-provider success is not live Tavily acceptance.

Native ingestion has typed recorded-fixture coverage. Current Pi/Codex
adapters still report `native_annotations: false`; a supported upstream
hook and separate live verification are required before changing that
capability. This is the intended scope of tasks 5.1/5.2.

Downstream Buda inline citation rendering, structured-first card parsing,
database persistence, reload/fork UI behavior, and hosted OpenAI search
acceptance remain separate. The consumer checklist maps these to explicit
follow-up tests. kapps PR #8009 implements retrieved-source cards and does
not implement this answer annotation contract. This change remains opt-in.
