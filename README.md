# Kinbox — a family document vault you can just ask

**An AI agent built on Amazon Bedrock.** Upload your family's important documents once, then just ask: *"When does my residence permit expire?"*, *"What's the engine number on the bike insurance?"*, *"Which documents expire this month?"* — and get the exact answer in a sentence, with the source document named.

**Built by [Mugesh Murugaiyan](https://github.com/Mugeshgithub) · CognivexAI**
`#agents`

**Live app:** https://kinbox-two.vercel.app

> **Note on the code:** The full source is kept private for security and commercial reasons, since Kinbox handles people's private documents. This repository is a public write-up and demo of the agent for the AWS "Build an agent people actually enjoy using" challenge.

---

## Demo

<!-- Drop the clip in ./media/ and it will show here -->
https://github.com/Mugeshgithub/kinbox-bedrock-agent/raw/main/media/kinbox-demo.mp4

*(Uploading a document, asking "what's my engine number?", and getting the exact answer with the source file named — all powered by Claude on Amazon Bedrock.)*

---

## What it is and who it's for

Kinbox is a private vault for the documents families actually need but can never find: passports, residence permits, insurance policies, car papers, tax notices. You upload them once, and then you just ask. It's built for ordinary families, and especially for people juggling paperwork across countries, like expats and new immigrants, where a missed renewal date has real consequences.

Instead of scrolling through ten-page PDFs, you get the exact answer in a sentence, with the source document named.

It's built for the whole family, not one person. You set up your vault, then **invite your family with a unique link**. They open the link, sign in, and join your shared space, so everyone can keep and find the household's documents together. The invite links are **single-use and expiring**, so access stays controlled.

## The biggest leverage: it watches your deadlines

Answering questions is useful, but the real value is that Kinbox is **proactive**. Every document is read for its expiry or renewal date, and those dates are surfaced for you automatically:

- Documents are shown **in a line with their expiry date**, and anything **expiring soon or already expired is flagged**, so you can see at a glance what needs attention.
- A daily job sends **reminders before a document expires** (30 days out, 7 days out, and on expiry), so a residence permit, insurance policy, or passport never lapses because someone forgot.

That turns Kinbox from a place you *search* into a quiet assistant that tells you what matters *before* it becomes a problem. For families managing paperwork across countries, a missed renewal can mean a fine, a lapse in cover, or a visa problem, so catching it early is the whole point.

## Privacy and security

Kinbox holds people's most sensitive documents, so privacy is built in, not bolted on:

- **Your conversations are not saved.** The assistant reads your documents to answer a question and keeps **no log** of what you asked. There is no chat history stored anywhere.
- **Data stays in the EU**, stored encrypted at rest in **private, per-family storage**.
- **Strict isolation:** row-level security means no family can ever see another family's documents, and the AI only ever has access to the asking user's own documents — so even a cleverly worded question can't reach anyone else's data.
- **Private by default:** identity, financial, and medical documents are automatically marked owner-only.

## How I built it

The agent runs on **Amazon Bedrock**, using **Claude Haiku 4.5** through Bedrock's **EU inference profile**, so inference stays in-region — which matters for a product holding people's private documents.

- **Document understanding:** When a document is uploaded, Claude (on Bedrock) reads it — PDF or photo — and extracts structured fields: document type, expiry date, and identifiers like policy, engine, and chassis numbers.
- **Retrieval:** **Voyage AI** embeddings stored in **Supabase** (Postgres with pgvector), so a question like *"what's my motor ID"* still finds *"engine number"* buried on page 10.
- **Isolation:** Row-level security keeps every family's data fully separated.
- **Answering:** The agent combines the extracted fields and the most relevant chunks, then Claude on Bedrock writes a short, grounded answer that names the file it came from.

The app is built with Next.js, is bilingual (English and French), and uses Google sign-in with per-user rate limiting so the assistant can't be abused.

**Stack:** Amazon Bedrock (Claude Haiku 4.5, EU) · Voyage AI embeddings · Supabase (Postgres + pgvector) · Next.js

## The delightful detail

Most document AI dumps a wall of text. I made Kinbox answer like a person who actually knows your files: short, specific, and honest. It gives you the exact number or date, it names the source document so you can trust it, and if it can't find something it says so instead of guessing. It also knows when to stay quiet — if you just say "thanks," it replies warmly in one line instead of repeating facts. Privacy is visible too: identity and financial documents are automatically marked private with an "Only you" badge, and a small welcome animation greets each family by name.

I knew it worked when I asked it for a chassis number from a document I'd forgotten the contents of, and it answered correctly in one line, pointing at the right PDF.

---

Built for the AWS Builder Center weekend challenge · `#agents`
