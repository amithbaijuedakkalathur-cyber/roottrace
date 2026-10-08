# RootTrace

**A Gemini-powered root-cause debugging workspace.**

[Open the live workspace](https://roottrace.amith-baiju.workers.dev/) · [Builder's portfolio](https://amith-baiju.netlify.app/)

This public repository is a product case study. Backend implementation, provider credentials and hosting internals are not included.

## The problem

A traceback identifies where execution failed, but often leaves the developer to reconstruct why the data reached that state. A plausible patch can suppress the symptom while preserving the underlying bug.

RootTrace asks for the traceback, failing code and optional related context, then presents a structured diagnosis for human review. Its intended contract is **evidence → root cause → minimal patch → verification guidance**, with uncertainty made visible.

## Implementation approach

The browser collects a small, relevant code path and an error report. The current live interface states that submitted code is sent to Gemini for analysis when connected. The owner confirmed Gemini as the current provider on 8 October 2026.

At the product level, the flow separates evidence collection, diagnosis, patch review and verification. A useful diagnosis must explain the failing data/control path, propose a focused change and identify missing context. A proposed patch is not automatically applied, and suggested verification is not evidence that tests ran.

No backend architecture, specific Gemini model, data-retention guarantee or server-side control is asserted here without implementation evidence.

## Demonstration

1. Open the live workspace.
2. Select **Load sample bug**.
3. Inspect `normalize_user`: it adds `user_id` only when `is_new=True`, while the caller uses the default `False` and then reads `user['user_id']`.
4. Select **Diagnose root cause**.
5. Review the diagnosis and proposed patch, then verify the intended behavior in your own environment.

The expected cause above follows directly from the sample code. It is not a claimed successful AI response.

### Verification on 8 October 2026

- The current Cloudflare URL loaded the debugging interface.
- **Load sample bug** populated the traceback, code and related context.
- The page displayed a 36,000-character input limit and a warning that code is sent to Gemini.
- The sample diagnosis request returned **“Gemini could not complete the diagnosis (upstream HTTP 503). Try again shortly.”**

The interface is accessible, but successful live diagnosis was not established in this check. No arbitrary-code accuracy, uptime, benchmark results or automated-test results are claimed. Earlier ChatGPT Sites deployments are not evidence of the current provider's behavior.

## Safeguards and limits

- Submit only minimal code you have permission to share, with secrets and identifying data removed.
- The UI says code is analyzed rather than executed; backend enforcement was not independently audited in this public repository.
- Keep credentials server-side and private. Never paste an API key into this repository or a public issue.
- Review every suggested patch and run relevant checks yourself. Model confidence is a signal, not a correctness guarantee.
- Provider failures must stay visible rather than being presented as successful AI output.
- Retention, rate limiting, structured-output validation, timeout behavior and abuse protection require backend verification before production-readiness claims.

## My contribution and status

I shaped the debugging workflow and product presentation through AI-assisted development. The public evidence supports a deployed developer-tool experiment, not a production debugging service or measured accuracy claim.

Next validation priorities are restoring reliable provider responses, checking distinct failures against known expected causes, testing malformed inputs and provider errors, and documenting dated results. These are planned checks, not completed results.

## Contact

[Amith Baiju E](https://amith-baiju.netlify.app/) · [LinkedIn](https://www.linkedin.com/in/amith-baiju/) · [Email](mailto:amithbaijuedakkalathur@gmail.com)
