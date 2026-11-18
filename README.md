# The AI Fixery · Free n8n Workflows

Practical, inspectable automation tutorials. We show what each workflow **actually does**, provide safe example data, and explain what is **not** included.

Watch tutorials on [The AI Fixery YouTube channel](https://www.youtube.com/@TheAIFixery).

## L01 — Safe Lead Triage (NO SEND)

**A deterministic JavaScript demo — not AI scoring, not a production lead-management system.**

This four-node n8n workflow:

- Starts with a manual trigger and generates five fictional leads.
- Scores urgency, budget, requested service, basic email format, and message length.
- Classifies each example as **HOT**, **WARM**, **LOW**, or **REVIEW**.
- Creates suggested reply **text** only; it does **not** send or save email drafts.
- Reports whether the five expected classifications pass a QA check.

It has **no credentials, webhooks, CRM connection, Gmail integration, external API, or outbound sending nodes**. The supplied QA cases all passed in the reference demonstration, but this is not a production-readiness or security certification.

### Download (recommended)

Open the repository's **Releases** page and download `L01_Free_n8n_Safe_Lead_Triage_v1.0.zip` from release **v1.0.0**. This ZIP includes the importable workflow, test data, usage instructions, and integrity checksums. Do **not** confuse GitHub's automatically generated “Source code (zip)” with the named starter ZIP release asset.

### Quick start

1. Create a **new** workflow in n8n, then import `N8N_Free_Lead_Triage_NO_SEND.json` from the downloaded ZIP.
2. Inspect the JavaScript nodes and confirm there are no credentials or external integrations.
3. Press **Execute workflow**; open the **QA Report** output.
4. For the five supplied synthetic cases, the expected output is `all_pass: true`, `passed: 5`, `total: 5`, with `outbound_sent: false` in every case.
5. To experiment, edit only the sample data and scoring weights, then test boundary cases and missing inputs.

### Scoring logic

| Rule | Points |
|---|---:|
| Urgency ≤1 day / 2–3 / 4–7 / later | 35 / 25 / 15 / 5 |
| Budget ≥€5,000 / €1,000–4,999 / below €1,000 | 25 / 15 / 0 |
| Requested service provided | 20 |
| Email matches a *basic* format pattern | 10 |
| Message length ≥40 characters | 10 |

An invalid email format or a missing requested service always yields **REVIEW**. Otherwise, ≥70 is HOT, ≥40 is WARM, and lower scores are LOW. A format check does **not** verify mailbox existence or deliverability.

### Safety limits

All leads in this repository are fictional. These scoring weights are illustrative, not validated sales predictions. Before any real deployment you would need customer-data privacy controls, authenticating inputs, handling retries and duplicates, monitoring, human review, and much broader testing. Never treat output flags alone as a security mechanism; the demo is safe from outbound sending because it contains **no sending actions**.

## License

MIT License for code and documentation in this repository. See `LICENSE`. Do not redistribute third-party trademarks or copyrighted media as if licensed by this repository.
