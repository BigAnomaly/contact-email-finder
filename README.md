[Contact Email Finder](https://apify.com/sovereigntaylor/contact-email-finder?fpr=data)

# Contact Details & Email Finder

Extract emails, phone numbers, social media profiles, and contact information from any website. Built for **lead generation**, **sales prospecting**, and **market research**.

## What It Does

Give it a list of website URLs and it will:

- **Find email addresses** from page content, mailto: links, meta tags, and structured data
- **Extract phone numbers** from page content, tel: links, and structured data (international formats supported)
- **Discover social profiles** for LinkedIn, Twitter/X, Facebook, Instagram, YouTube, and GitHub
- **Auto-crawl contact pages** by detecting /contact, /about, /team, /people, /impressum pages
- **Parse structured data** from JSON-LD (schema.org Organization, LocalBusiness) for verified contact info
- **Discover email patterns** by trying common prefixes (info@, contact@, hello@, support@, sales@)
- **Extract company details** including name, address, and all discovered contact pages

## Use Cases

### Sales & Lead Generation

Build targeted lead lists by scraping contact details from prospect websites. Feed the results directly into your CRM or outreach tool.

### Competitor Research

Extract contact information from competitor websites to understand their team structure and communication channels.

### Business Directory Building

Crawl industry websites to build comprehensive business directories with verified contact details.

### Recruitment

Find contact details for companies you want to reach out to, including LinkedIn profiles of key team members.

### Market Research

Map out companies in a specific niche by extracting their contact details and social presence.

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `urls` | array | required | List of website URLs to extract contacts from |
| `maxDepth` | integer | 3 | How deep to crawl (0 = start URL only) |
| `includeEmails` | boolean | true | Extract email addresses |
| `includePhones` | boolean | true | Extract phone numbers |
| `includeSocials` | boolean | true | Extract social media profile links |
| `emailPatterns` | boolean | true | Try common email patterns for the domain |
| `maxResults` | integer | 500 | Max number of websites to process |
| `proxy` | object | Apify Proxy | Proxy configuration |

### Example Input

```
{
  "urls": [
    "https://example.com",
    "https://another-company.com"
  ],
  "maxDepth": 3,
  "includeEmails": true,
  "includePhones": true,
  "includeSocials": true,
  "emailPatterns": true,
  "maxResults": 500
}
```

## Output

Each result contains all contact details found for one website:

```
{
  "url": "https://example.com",
  "companyName": "Example Inc.",
  "emails": [
    "info@example.com",
    "sales@example.com",
    "john.smith@example.com"
  ],
  "phones": [
    "+1 (555) 123-4567",
    "+44 20 7946 0958"
  ],
  "socialProfiles": {
    "linkedin": "https://linkedin.com/company/example",
    "twitter": "https://twitter.com/example",
    "facebook": "https://facebook.com/example",
    "instagram": "https://instagram.com/example",
    "youtube": "https://youtube.com/c/example",
    "github": "https://github.com/example"
  },
  "address": "123 Main Street, San Francisco, CA 94105",
  "contactPages": [
    "https://example.com/contact",
    "https://example.com/about"
  ],
  "extractedAt": "2026-03-01T12:00:00.000Z"
}
```

## Extraction Strategies

The actor uses 6 layered strategies to maximize contact discovery:

1. **Direct Page Crawling** -- Scans page content and HTML for emails, phones, and links
2. **Contact Page Discovery** -- Automatically finds and crawls /contact, /about, /team pages
3. **Social Media Extraction** -- Identifies links to all major social platforms
4. **Email Pattern Discovery** -- Tests common email prefixes against the domain
5. **Structured Data Parsing** -- Extracts verified info from JSON-LD schema.org markup
6. **Meta Tag Mining** -- Parses og:email, schema.org itemprops, and other metadata

## Pricing

This actor uses **Pay Per Event** pricing:

- **$0.008 per website** where contact details are successfully found
- You only pay when contacts are actually discovered
- No charge for websites where no contacts are found

## Tips for Best Results

- **Start with the homepage** -- The actor will auto-discover contact pages from there
- **Set maxDepth to 2-3** -- This covers most contact pages without over-crawling
- **Use Apify Proxy** -- Avoid getting blocked, especially when scraping many sites
- **Batch your URLs** -- Process hundreds of websites in a single run for efficiency
- **Check contactPages** -- The discovered pages often contain additional details not captured in structured fields

## Integrations

Export results directly to:

- Google Sheets
- Excel / CSV
- Webhook (real-time delivery)
- Zapier / Make / n8n
- Any CRM via API

## Support

Found a bug or have a feature request? Open an issue on the actor's page or contact the author.