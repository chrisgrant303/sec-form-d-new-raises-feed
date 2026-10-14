# SEC Form D Scraper – New Startup Funding Raises Feed

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-00a86b)](https://apify.com/cce_partners/sec-form-d-new-raises-feed)

**▶ Try it on the Apify Store: https://apify.com/cce_partners/sec-form-d-new-raises-feed**

SEC Form D Scraper is a **startup funding feed** built on official SEC EDGAR data. Each run returns only the **new** Form D filings (Regulation D private placements: startup rounds, fund raises, real-estate syndications). It outputs clean, flat rows with the offering amount and amount sold already parsed, and no personal names.

Form D is filed within 15 days of a Reg D sale, so it's the earliest public signal that a company or fund just raised money, often before any press release. Schedule it daily and send **new funding alerts** to Google Sheets, Slack, HubSpot, Zapier, Make, n8n or any webhook.

> This repo contains documentation and examples only. The Actor runs on Apify: **[open the Apify Store listing](https://apify.com/cce_partners/sec-form-d-new-raises-feed)**.

## What it does
- **Returns new filings only.** Delta mode remembers what each `stateKey` has already delivered, so a daily schedule gives you a clean list of who just raised.
- **Parses the amounts for you.** Total offering amount, amount sold and amount remaining come straight from each filing's XML.
- **Filters** by issuer state, industry group, minimum offering amount and a CIK watchlist, with optional amendments (D/A).
- **Is private by design.** Executives, directors, promoters and signers are never output; only issuer and offering fields pass a whitelist.
- **Uses official sources only.** It reads the EDGAR daily index and each filing's `primary_doc.xml` with a declared User-Agent, at 5 requests/second (under the SEC's 10/s limit), with retries. No API key needed.

## Who it's for
- VC and fintech teams doing **deal sourcing**
- B2B sales teams prospecting **recently funded companies**
- Startup-funding newsletters and researchers
- Developers who want an **EDGAR Form D API** without maintaining SEC parsing code

## Example input
```json
{
  "states": ["CA", "NY"],
  "industryGroups": ["Other Technology"],
  "minOfferingAmount": 2000000,
  "stateKey": "sales-tech-ca-ny"
}
```
Leave `dateFrom` empty for delta mode. Set `dateFrom` / `dateTo` for a one-off backfill.

## Sample output fields
| Field | Example |
|---|---|
| `issuerName` | `222 Show Ltd Liability Co` |
| `cik` | `2157448` |
| `formType` / `isAmendment` | `D` / `false` |
| `state` / `stateDescription` | `NY` / `NEW YORK` |
| `entityType` | `Limited Liability Company` |
| `industryGroup` | `Other Technology` |
| `totalOfferingAmount` / `totalOfferingIndefinite` | `2400000` / `false` |
| `totalAmountSold` / `totalRemaining` | `622000` / `1778000` |
| `dateOfFirstSale` / `filingDate` | ISO dates |
| `accessionNumber`, `filingUrl`, `primaryDocUrl` | Links to sec.gov |

There are no person fields (no executives, promoters, signers or sales-compensation recipients).

## Pricing (pay per event)
- **$0.01** per run
- **$0.005** per filing returned ($5 per 1,000)

Use `maxFilings` to cap the cost of each run. See current pricing on the [Apify Store listing](https://apify.com/cce_partners/sec-form-d-new-raises-feed).

## How to set up daily funding alerts
1. Open the [Actor on Apify](https://apify.com/cce_partners/sec-form-d-new-raises-feed) and click **Try for free**.
2. Set your filters and a `stateKey` name.
3. Add a **Schedule** (for example, daily at 7 AM) and an integration (Google Sheets, Slack, HubSpot, webhook).

## FAQ
**Do I get duplicates?** Not in delta mode. Each `stateKey` remembers which filings it has delivered.
**Does it scrape web pages?** No. It uses EDGAR's published daily index and filing XML.
**Does a Form D mean the round closed?** No. It's a notice of an exempt offering, and "amount sold" is what the issuer reported. Not investment advice.

---
Published by [CCE Partners](https://apify.com/cce_partners). Not affiliated with the SEC.
**→ [SEC Form D Scraper on Apify Store](https://apify.com/cce_partners/sec-form-d-new-raises-feed)**
