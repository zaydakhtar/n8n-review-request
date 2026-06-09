# Automated Review Request System

An n8n workflow that automatically sends AI-personalised review request emails to customers after a completed job or appointment — helping small businesses build their online reputation on autopilot.

---

## The Problem

Most small businesses know they should ask for reviews. Almost none do it consistently.

After a busy day, following up with every customer individually is the last thing on anyone's mind. Reviews don't get requested, reputation doesn't grow, and new customers choose competitors with better ratings instead.

---

## The Solution

This workflow triggers automatically when a job is marked complete. It waits a set period, then uses Groq to write a warm, personalised review request email and sends it via Brevo. Every request is logged to Google Sheets and confirmed via Telegram.

No manual follow-up. Every completed job becomes a review opportunity.

---

## How It Works

1. **Job complete trigger** — webhook receives customer and job details on completion
2. **Timed delay** — workflow waits 2 hours before sending (configurable)
3. **AI email generation** — Groq (LLaMA 3) writes a personalised, natural-sounding review request
4. **Email sent** — Brevo delivers the email from the business's address
5. **Logged to Google Sheets** — request recorded with timestamp and customer details
6. **Telegram confirmation** — owner notified that the review request was sent

---

## Stack

| Tool | Role |
|------|------|
| n8n (self-hosted) | Workflow orchestration |
| Groq (LLaMA 3) | AI email personalisation |
| Brevo | Email delivery |
| Google Sheets | Request logging and tracking |
| Telegram | Owner confirmation alerts |

---

## Use Case

- Every completed job automatically triggers a review request
- Emails feel personal and genuine — not templated
- 2-hour delay hits the sweet spot when the customer experience is still fresh
- Full log of every request sent, queryable in Google Sheets
- Designed for UK hair salons, independent restaurants, and sole-trader trades

---

## Setup

### Prerequisites
- n8n instance (self-hosted or cloud)
- Groq API key (free tier works)
- Brevo account with a verified sender email (free tier works)
- Google Sheets with service account or OAuth credentials
- Telegram bot token
- Google Sheet with a tab named `Review Requests`

`Review Requests` tab columns: `Timestamp`, `Customer Name`, `Customer Email`, `Job Type`, `Business Name`, `Email Subject`, `Status`

### Installation

1. Clone or download this repo
2. Import `workflow/review-request.json` into your n8n instance
3. Copy `.env.example` to `.env` and fill in your credentials
4. In n8n, create a Header Auth credential named `Groq API Key` — header: `Authorization`, value: `Bearer YOUR_GROQ_API_KEY`
5. Create a Header Auth credential named `Brevo API Key` — header: `api-key`, value: `YOUR_BREVO_API_KEY`
6. Connect your Google Sheets and Telegram credentials
7. In the `Send Email via Brevo` node, replace `YOUR_SENDER_EMAIL` with your verified Brevo sender address
8. Set your Google Sheet ID in the Sheets node
9. Set your Telegram Chat ID in the Telegram node
10. Activate the workflow

See `.env.example` for all required environment variables.

### Triggering the Workflow

Send a POST request to your webhook URL with this JSON body:

```json
{
  "customerName": "Sarah Johnson",
  "customerEmail": "sarah@example.com",
  "jobType": "haircut and colour",
  "businessName": "The Style Room"
}
```

---

## Project Status

✅ Built and tested
🧪 Demonstration build — fully functional, available to deploy
📍 Designed for UK small business use cases

---

## Author

**Zayd Akhtar** — AI Automation Builder
[LinkedIn](https://www.linkedin.com/in/zayd-a-03b681144/) · [GitHub](https://github.com/zaydakhtar)
Open to remote contracts and consulting · Based in the UK
