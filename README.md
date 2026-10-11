# Kinbox — a family document vault you can just ask

**An AI agent built on Amazon Bedrock.** Upload your family's important documents once, then just ask: *"When does my residence permit expire?"*, *"What's the engine number on the bike insurance?"*, *"Which documents expire this month?"* — and get the exact answer in a sentence, with the source document named.

**Built by [Mugesh Murugaiyan](https://github.com/Mugeshgithub) · CognivexAI**
`#agents`

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
