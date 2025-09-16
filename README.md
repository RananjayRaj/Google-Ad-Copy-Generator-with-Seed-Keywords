# README.md

````
# Google Ads Ad Copy Generator (n8n) — SANITIZED

This repository contains a sanitized n8n workflow export for **Google Ads Ad Copy Generator from Seed Keywords (Advanced)**.

> ⚠️ **Important:** This repository is intentionally sanitized. All credential IDs, instance metadata, webhook IDs and direct document URLs have been replaced with placeholders. Before using the workflow you must attach your own credentials and replace placeholders.

---

## Files in this repo

- `Google Ads Ad Copy Generator from Seed Keywords Advanced.json` — the sanitized n8n workflow (importable into n8n).
- `.env.example` — environment variable examples for local reference.
- `README.md` — this file.

---

## Quick start (import + configure)

1. **Clone the repo**
   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
````

2. **Import workflow into n8n**

   * Open your n8n instance (self-hosted or cloud).
   * Click **Import** -> **From File** and choose `Google Ads Ad Copy Generator from Seed Keywords Advanced.json`.

3. **Create credentials in n8n**
   In your n8n instance create the following credentials (example names are suggestions):

   * **Google Sheets OAuth2** — name: `Google Sheets account` (used to access target spreadsheet)
   * **OpenAI API** — name: `OpenAi account` (or equivalent LLM provider credential)

   After creating credentials, open the imported workflow and attach the credentials to the respective nodes via the node UI (click node -> Credentials -> select credential).

4. **Replace placeholders**
   The sanitized JSON contains placeholders you must replace either via the n8n UI (recommended) or by editing the JSON file directly before importing.

   Common placeholders in `Google Ads Ad Copy Generator from Seed Keywords Advanced.json`:

   * `REPLACE_GOOGLE_SHEET_ID` — replace with your Google Sheets spreadsheet ID (the long ID in the sheet URL)
   * `REPLACE_GOOGLE_SHEETS_CREDENTIAL_ID` & `REPLACE_GOOGLE_SHEETS_CREDENTIAL_NAME` — placeholders inside `credentials` blocks (safe to ignore if you attach credentials manually in the n8n UI)
   * `REPLACE_OPENAI_CREDENTIAL_ID` & `REPLACE_OPENAI_CREDENTIAL_NAME` — same as above for OpenAI/LLM credentials

   **Recommended method:** attach credentials inside n8n UI (no JSON edits). For sheet IDs, edit the node parameter `documentId.value` and paste your real sheet ID.

5. **(Optional) Use environment variables**
   If you prefer environment-driven configuration, you can store API keys in environment variables (for example: `OPENAI_API_KEY`, `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`) and configure n8n credentials to use those environment values. See `.env.example` for suggested variable names.

6. **Test the workflow**

   * Run the form trigger node (or create a temporary test input) to ensure the pipeline runs through generating keywords and ad copy and writing to the sheet.

---

## Mapping: placeholders → where to set them

| Placeholder in JSON                                                             |                         What it is | How to replace it                                                                                      |
| ------------------------------------------------------------------------------- | ---------------------------------: | ------------------------------------------------------------------------------------------------------ |
| `REPLACE_GOOGLE_SHEET_ID`                                                       |       Google Sheets spreadsheet ID | In node `Google Sheets` → `documentId.value` or in the Google Sheets node UI input field.              |
| `REPLACE_GOOGLE_SHEETS_CREDENTIAL_ID` / `REPLACE_GOOGLE_SHEETS_CREDENTIAL_NAME` |            n8n credential metadata | Create a Google Sheets OAuth2 credential in n8n, then in the node UI select it. No JSON edit required. |
| `REPLACE_OPENAI_CREDENTIAL_ID` / `REPLACE_OPENAI_CREDENTIAL_NAME`               |    n8n credential metadata for LLM | Create the OpenAI (or LLM) credential in n8n and attach it in the OpenAI node.                         |
| `REDACTED_GOOGLE_DOC_URL`                                                       | Previously linked doc URL redacted | Not required. If needed, add your own URLs through node params.                                        |

---

## Security notes

* **Do not commit real credentials** to the repo. Use n8n's credential store and the UI to attach credentials.
* If you ever accidentally commit an API key or token, **revoke/rotate** it immediately.
* Keep secrets out of code nodes. If you must reference keys in code, use environment variables and read them at runtime.

---

## Customization tips

* If you prefer to have the workflow read values from environment variables, create an initial `Set` node that reads from environment variables (via expression syntax) and passes the values downstream. But prefer attaching credentials in the n8n credentials UI.
* If using a team or sharing the repo publicly, add documentation on the exact names of the credentials you expect contributors to create.

---

## License

This repo includes a sample workflow. Choose a license for your repo before publishing. A commonly used permissive license is the MIT license. Example `LICENSE` (MIT) can be added if you want others to reuse freely.

---

## Troubleshooting

* **Workflow failing at Google Sheets node**: confirm the Sheets credential is attached and the `documentId` refers to a sheet the service account / user has access to.
* **OpenAI node errors**: ensure your OpenAI credential is configured in n8n and that rate limits/quota are available.
* **Webhook not firing**: webhook IDs were nulled in the sanitized export. Recreate trigger webhooks by enabling the trigger node and copying the new webhook URL from n8n.

---

## Contributing

If you accept contributions, add a `CONTRIBUTING.md` describing naming conventions for credentials and how to test new changes locally.

```
