[Bulk Email Verifier](https://apify.com/solutionssmart/bulk-email-verifier?fpr=data)

# 📧 Bulk Email Verifier

Clean your email lists, reduce bounce risk, and protect your sender reputation.

Bulk Email Verifier is an Apify Actor for validating large lists of email addresses before you use them in cold outreach, CRM imports, or automation workflows. It checks each email with practical verification steps and returns structured results you can use immediately in your pipeline.

It is built for affordable bulk verification without paid third-party verification APIs.

## 🚀 Why use this actor?

If you run:

- cold email campaigns
- lead generation workflows
- CRM imports
- marketing automation
- scraped lead pipelines

bad email data creates avoidable problems:

- higher bounce rates
- weaker sender reputation
- wasted credits in outreach tools
- low-quality CRM records
- more manual cleanup work

Bulk Email Verifier helps you clean the list before sending, importing, or syncing it elsewhere.

## ✅ What this actor checks

Each email goes through several validation steps:

- Syntax validation: checks whether the email format is valid
- DNS / MX validation: checks whether the domain can receive email
- Disposable email detection: flags temporary or throwaway email providers
- Role account detection: flags generic inboxes like `info@`, `sales@`, or `admin@`
- Free provider signal: marks addresses from providers like Gmail or Yahoo as a separate signal

The actor labels each email as one of these statuses:

- `valid`
- `risky`
- `invalid`
- `unknown`

## 🎯 Typical use cases

### 🔎 Lead generation

Verify email lists collected from:

- Google Maps scraping workflows
- LinkedIn lead collection workflows
- website contact extraction
- business directory scraping

### ✉️ Cold outreach

Clean email lists before sending campaigns with tools such as:

- Instantly
- Lemlist
- Mailshake
- Smartlead
- other outreach platforms

### 🗂️ CRM and list cleanup

Validate contacts before importing into:

- HubSpot
- Pipedrive
- Salesforce
- Airtable
- internal sales databases

### ⚙️ Automation workflows

Use the actor inside:

- Apify pipelines
- n8n
- Make
- Zapier
- custom API workflows

## 📥 Input options

You can provide email lists in several beginner-friendly ways:

- Inline email array
- CSV file available at a public URL
- Raw CSV pasted directly into input
- Apify Dataset from another actor
- Apify Key-Value Store record

Provide either `emails` or `source`, not both.

## ⚡ Try it in 30 seconds

Use this small test input to verify a few emails quickly:

```
{
  "emails": [
    "contact@company.com",
    "info@startup.io",
    "hello@gmail.com"
  ],
  "mode": "mx",
  "dedupe": true,
  "checkDisposable": true,
  "checkRoleAccounts": true,
  "output": {
    "format": "dataset",
    "includeReasoning": true
  },
  "limits": {
    "maxEmails": 10,
    "concurrency": 5
  }
}
```

This example is also available in examples/input-inline.json.

## 🧩 Example inputs

The actor uses `mode: "mx"` for MX validation, `checkRoleAccounts` for role inbox detection, and `source` for CSV or dataset inputs. The examples below match the current input schema, so they can be pasted directly into the actor.

### Example 1: Quick Email Check

**Title**

Quick Email Validation

**Description**

Verify a small list of emails before sending a campaign.

**Input JSON**

```
{
  "emails": [
    "contact@company.com",
    "info@startup.io",
    "hello@gmail.com"
  ],
  "mode": "mx",
  "checkDisposable": true,
  "checkRoleAccounts": true,
  "output": {
    "format": "dataset",
    "includeReasoning": true
  }
}
```

### Verify emails from CSV

```
{
  "source": {
    "type": "urlCsv",
    "url": "https://example.com/leads.csv"
  },
  "mode": "mx",
  "checkDisposable": true,
  "checkRoleAccounts": true,
  "output": {
    "format": "dataset,csv",
    "includeReasoning": true
  }
}
```

The Actor automatically uses the `email` column if it exists, or the first column otherwise.

### Verify emails from another dataset

```
{
  "source": {
    "type": "apifyDataset",
    "datasetId": "DATASET_ID"
  },
  "mode": "mx",
  "checkDisposable": true,
  "checkRoleAccounts": true,
  "output": {
    "format": "dataset,csv",
    "includeReasoning": true
  }
}
```

If the dataset contains an `email` field, the Actor uses it automatically. If not, it falls back to the first field in each item.

## 📤 Example output

Each verified email is stored as one item in the default dataset.

```
{
  "email": "john@example.com",
  "status": "valid",
  "reasons": [],
  "signals": {
    "syntaxOk": true,
    "mxOk": true,
    "mxRecords": [
      {
        "exchange": "mail.example.com",
        "priority": 10
      }
    ],
    "isDisposable": false,
    "isRole": false,
    "isFreeProvider": false,
    "domain": "example.com"
  },
  "timing": {
    "normalize": 0,
    "syntax": 0,
    "mx": 42,
    "heuristics": 1
  },
  "reasoning": "Syntax and MX OK; no risky signals."
}
```

## 📊 Output fields

| Field | Description |
| --- | --- |
| `email` | Normalized email address |
| `status` | Final classification: `valid`, `risky`, `invalid`, or `unknown` |
| `reasons` | Reason codes such as `invalid_syntax`, `no_mx`, `disposable_domain`, `role_account`, or `smtp_rejected` |
| `signals` | Detailed machine-readable verification signals |
| `timing` | Per-step timing information in milliseconds |
| `reasoning` | Human-readable explanation when enabled |

Results can be consumed from the default dataset and exported as JSON, CSV, Excel, or API responses.

If you set `output.format` to `dataset,csv`, the Actor also saves `results.csv` to the default Key-Value Store. Every run also saves a `SUMMARY` record with aggregate counts and output settings.

## 🛠️ Recommended setup

For most use cases:

- use `mode: "mx"`
- keep `checkDisposable: true`
- keep `checkRoleAccounts: true`
- enable CSV output when you want a ready-to-import file

`smtp` mode is experimental. If you use it, also set `enableSmtp: true`.

## ▶️ How to use

1. Open the Actor in Apify.
2. Add emails directly or connect a source such as a CSV URL or dataset.
3. Choose the verification mode. `mx` is the recommended default.
4. Start the run.
5. Review the dataset results and export or forward the contacts you want to keep.

## Built for automation

Bulk Email Verifier is designed to work well inside data pipelines.

```
Lead Scraper
     ->
Bulk Email Verifier
     ->
CRM / Outreach Tool
```

You can also send result batches to your own endpoint using the built-in webhook option.

## 💰 Pricing

The Actor uses Apify's consumption-based pricing, so cost depends on list size, concurrency, and DNS response times.

Because the Actor does not rely on paid verification APIs, it is generally a low-cost option for bulk pre-verification and list cleaning.

## 👥 Who should use this actor?

This Actor is a practical fit for:

- marketers
- growth teams
- lead generation agencies
- sales operations teams
- automation engineers
- Apify users building scraper-to-CRM workflows

## 🤝 Support

If you need help or want to suggest improvements:

- use the repository issue tracker
- use the Actor Issues tab on Apify
- send feature requests for new workflow integrations or output formats

Feedback is welcome, especially from teams using the Actor in real lead generation and outreach pipelines.