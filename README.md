[Bulk Email Verifier](https://apify.com/codescraper/bulk-email-verifier?fpr=data)

# 🔗 Bulk Email Verifier – Validate and Analyze Emails

This **Apify actor** verifies email addresses and returns detailed insights about deliverability, quality, sender info, domain info, risk, and breaches Using Abstract Api Email Reputation Api keys.

It supports single emails or lists of emails, validates MX/SMTP records, and provides a quality score for each address.

---

## 🚀 What It Does

The actor processes each email address and returns a comprehensive profile including:

- 📧 **Email Info:** Address, Deliverability Status, Score, and Role/Disposable flags
- 🛡️ **Validation:** Format, SMTP, and MX record checks
- 🏢 **Sender Info:** Provider, Organization, First/Last Name (if available)
- 🌐 **Domain Info:** Domain age, registrar, registration/expiry dates, TLD risk
- ⚠️ **Risk Assessment:** Address & domain risk status
- 🔓 **Breaches:** Total breaches, dates, and breached domains

## ⚡ It handles

- ✅ Bulk email lists or single addresses
- 🔄 Automatic MX & SMTP verification
- 🛡️ Risk & breach checks for informed decision making

---

## 🔑 Using Your Own Abstract API Key (Optional)

providing your own API key allows higher request limits:

- Go to Abstract API Email Reputation: [https://app.abstractapi.com/api/email-reputation/tester](https://app.abstractapi.com/api/email-reputation/tester)
- Sign up for a free account or log in if you already have one.
- Your key will be auto generated check section email-reputation. make sure you are at this link

[https://app.abstractapi.com/api/email-reputation/tester](https://app.abstractapi.com/api/email-reputation/tester)
- Copy the key named as Primary Key.
- Free tier allows 100 email validations per month.
- You can upgrade to paid plans for additional requests.
- Add the key to the Your API Key field when running the actor.

⚠️ If no key is provided, the actor will automatically use its own keys. Remember if actor ran out of

api key credits you need to enter your own api key

## ⚙️ Input Configuration

| Field | Type | Description | Default Example |
| --- | --- | --- | --- |
| `emails` | Array | Enter a list of email addresses to verify | `["test@gmail.com", "info@company.com"]` |

---

## 🧩 Example Input

```
{
  "emails": ["compiledcurious@gmail.com", "example@mycompany.com"]
  "Your API Key(Optional)": "YOUR_ABSTRACT_API_KEY_HERE"
}
```

---

## 📊 Example Output

```
[
  {
    "email_address": "compiledcurious@gmail.com",
    "success": true,
    "summary": {
      "status": "deliverable",
      "score": "0.95",
      "is_disposable": false,
      "is_role": false,
      "mx_records": [
        "gmail-smtp-in.l.google.com",
        "alt1.gmail-smtp-in.l.google.com",
        "alt2.gmail-smtp-in.l.google.com",
        "alt3.gmail-smtp-in.l.google.com",
        "alt4.gmail-smtp-in.l.google.com"
      ],
      "domain": "gmail.com"
    },
    "raw": {
      "email_deliverability": {
        "status": "deliverable",
        "status_detail": "valid_email",
        "is_format_valid": true,
        "is_smtp_valid": true,
        "is_mx_valid": true,
        "mx_records": [
          "gmail-smtp-in.l.google.com",
          "alt1.gmail-smtp-in.l.google.com",
          "alt2.gmail-smtp-in.l.google.com",
          "alt3.gmail-smtp-in.l.google.com",
          "alt4.gmail-smtp-in.l.google.com"
        ]
      },
      "email_quality": {
        "score": "0.95",
        "is_free_email": true,
        "is_username_suspicious": false,
        "is_disposable": false,
        "is_catchall": false,
        "is_subaddress": false,
        "is_role": false,
        "is_dmarc_enforced": true,
        "is_spf_strict": false,
        "minimum_age": null
      },
      "email_sender": {
        "first_name": null,
        "last_name": null,
        "email_provider_name": "Google",
        "organization_name": "Gmail",
        "organization_type": "commercial"
      },
      "email_domain": {
        "domain": "gmail.com",
        "domain_age": 11044,
        "is_live_site": true,
        "registrar": "MarkMonitor Inc.",
        "registrar_url": "https://markmonitor.com",
        "date_registered": "1995-08-13",
        "date_last_renewed": "2024-07-11",
        "date_expires": "2025-08-12",
        "is_risky_tld": false
      },
      "email_risk": {
        "address_risk_status": "low",
        "domain_risk_status": "low"
      },
      "email_breaches": {
        "total_breaches": 0,
        "date_first_breached": null,
        "date_last_breached": null,
        "breached_domains": []
      }
    }
  }
]
```

---

## 🧠 Features

- 📧 Verify **single or multiple emails**
- 🛡️ Checks **deliverability** (format, SMTP, MX)
- 🔍 Provides **quality analysis** (free, disposable, catch-all, role)
- 🏢 Extracts **sender info** (provider, organization, first/last name)
- 🌐 Retrieves **domain details** (age, registrar, registration & expiry, TLD risk)
- ⚠️ Risk & breach assessment for informed decisions
- 📊 Returns **MX records** and **summary score**

---

## 💡 Use Cases

- **Sales & Outreach:** Verify prospect email lists
- **Marketing:** Ensure deliverable emails for campaigns
- **Security:** Identify risky, disposable, or role-based addresses
- **Data Enrichment:** Add email quality & domain info to datasets

---

## 🧑‍💻 Developer Info

**Author:** [codescraper](mailto:codescraper011@gmail.com)

---

## 🏷️ Tags

`bulk-email-verifier` . `email-verification` · `email-validation` . `email-scraper` · `data-validation` · `email-quality` · `risk-assessment` · `apify` · `automation`