<!-- CLASSIFICATION: PUBLIC · MetawatchPHR — product document (EN) -->

# MetawatchPHR
### Your entire medical history. One timeline. Your machine only.

**Document version:** v1.1 DRAFT — Owner review owed · **2026-08-10** (v1.1: Release-information section added from the Architect's lifted draft sections, facts-card-checked; Epic line tightened to the provable claim) · Applies to: MetawatchPHR 0.2.0 (Windows beta; macOS in preparation) — re-stamps at the designated public release

---

## The problem nobody talks about

Your medical history is scattered across every clinic, hospital, lab, and specialist you have ever visited. Each one holds a fragment. Portals show you one hospital's slice. Old records live in boxes, PDFs, email attachments, and CDs in a drawer.

**The only person who has been present for your entire medical life is you** — and until now, you had no way to hold it all in one place, let alone read it as one story.

## What MetawatchPHR does

MetawatchPHR is a personal health record application that runs entirely on your own computer. You point it at the folder where your medical files live — PDFs, scanned letters, Word documents, lab spreadsheets, hospital exports, even medical imaging discs — and it reads them the way a meticulous clinician would.

Out the other side comes something you have never had before: **your complete health history as a single, organized, searchable timeline.**

- **Every visit, every result, in order.** Decades of paper and PDFs become one chronological record you can actually navigate.
- **Organized the way medicine is organized.** Your records sort themselves into clinical domains — cardiology, neurology, labs and vitals, imaging — so you browse your history the way a hospital chart reads, not the way a folder of PDFs piles up.
- **Built-in graphs, with the normal range drawn in.** Your lab results are charted over the years **against their reference range** — the band your doctor compares them to — so an out-of-range result stands out on sight, and a slow drift that developed across a decade, invisible in any single report, becomes obvious in one glance.
- **One event, one record — no matter how many copies you have.** Real medical folders are full of duplicates: the same lab report downloaded twice, the same visit summary from two portals. MetawatchPHR recognizes them and keeps **one** authoritative record instead of three copies cluttering your timeline.
- **Search everything — then narrow to exactly where you mean.** One search box runs across your entire history at once; one click filters the same search to a single domain. *"Stent"* across everything, or *"stent"* in cardiology only. When was that MRI? What did the cardiologist say in 2015? Seconds, not shoeboxes.
- **Your current state at a glance.** The top of your dashboard is a live summary the way a physician would want it: active problems, current medications with their purpose, and vitals — assembled from your records, always one look away.
- **Every record shows you where it came from.** Each entry carries its source — a hospital system, a scanned document, or the AI's reading of one — with anything AI-derived clearly labelled, and a tamper-evident seal that flags any record changed outside the application. You never have to wonder whether you're looking at the original truth.
- **Reports you can hand to a person.** One click produces a plain-language summary drawn from your own assembled record — your history, distilled for a new specialist, a caregiver, or yourself — always clearly marked as AI-written, and never a diagnosis: it summarizes what your records say, full stop.
- **Visit notes rewritten the way doctors write them.** Messy ten-page documents are distilled into a **SOAP note** — the standard format used in clinics everywhere: **S**ubjective (what you reported), **O**bjective (what was measured and found), **A**ssessment (what it was judged to be), **P**lan (what happens next). Your chaotic paperwork ends up in the same professional structure your physician keeps.
- **A built-in viewer for hospital imaging.** Those X-ray and scan discs the hospital hands you? MetawatchPHR reads them, files them into your timeline, and opens the images in its own viewer — no special radiology software required.
- **The whole family.** Multiple users on one machine, with strict walls between each person's records. Built for the person who manages a household's health, not just their own.
- **In your language.** Fully bilingual — French and English, throughout.

A built-in demo patient comes with every install, so you can explore everything before adding a single record of your own.

## The part that makes it different: your data never leaves your machine

Most health apps are a website wearing a mask — your records go to their servers, their cloud, their business model.

**MetawatchPHR has no cloud.** There is no account to create, no upload, no server holding your history. The application — including its AI — runs entirely on your own computer. The AI that reads your records is a model *you* run locally; your documents are never sent to anyone, for any reason.

We cannot lose your data in a breach, because we never have it. We cannot sell your data, because it never reaches us. That is not a policy promise that could change next year — **it is how the product is built.**

And your records remain yours in the most literal sense: they live in ordinary, readable files in one folder on your machine. Even uninstalling the application leaves your records untouched — only you can delete them.

## Powered by real medical standards

Under the hood — and you never need to look there — MetawatchPHR speaks the same technical languages hospitals do: the international standards for health records, lab codes, clinical documents, and medical imaging. That is what makes your timeline clinically coherent instead of a pile of text: the same blood test from three different labs lands as one comparable series, not three unrelated numbers.

It is also what makes your record **portable**. Your history is stored in an open, structured, human-readable format — never locked inside our application.

## Simple, honest pricing

- **The product is free. Forever.** The full refinery — reading your files, the timeline, the charts, the search, the summaries — costs nothing, with no trial, no limits, and no subscription.
- **Optional connectors, paid once.** Direct import lanes for hospital systems — starting with **Epic**, whose exports import by exact rules, no AI involved — are **$5 per connector, or $10 for all of them. One-time.** Not per month. Not per year. Once.
- The only network call the product ever makes is the moment a purchased connector validates its license — a call that contains no health data at all.

## Who it's for

- **The family caregiver** holding a parent's decades of records together.
- **Anyone managing a chronic condition** across multiple specialists who don't talk to each other.
- **The health-conscious** who want their labs, wearables, and history in one longitudinal picture.
- **Anyone who has ever left a specialist's office** with a folder of paper and the thought: *someone should keep track of all this.* Someone finally can — you.

## Getting started

1. Download the installer and run it.
2. Accept the agreements — presented in full, French or English.
3. Point MetawatchPHR at the folder holding your medical files.
4. Click **Scan Now**, and watch your history assemble itself.

A free local AI application (LM Studio) does the reading on your machine — the manual walks you through it in minutes.

---

## Release information — Windows beta

*(Sections below drafted by the Architect 2026-08-10, checked against the facts-of-record card; lifted per his "ready to lift" note with the filename form corrected to the build-code identity.)*

### System requirements

- **Windows 10 or 11, 64-bit.** About 600 MB of disk space.
- **Nothing else to install.** MetawatchPHR carries everything it needs — you do not need Python, Node, or any developer tools.
- **For the AI features** (record extraction, the clinical summary): a local AI server such as **LM Studio** (free) running one of the supported models on your machine or your own network. Without one, MetawatchPHR still works as a viewer for already-imported records.
- Your health data **never leaves your computer** except where you explicitly authorize it (see the privacy paragraph below).

### Installing

1. Download `MetawatchPHR-Setup-0.2.0-<build code>.exe` from the Releases page and run it. (The code at the end of the filename identifies the exact build — quote it in any support request.)
2. Windows may show **"Windows protected your PC"** — this beta is not yet code-signed. Click **More info → Run anyway**. (Signing is planned; this warning does not indicate a problem with the software.)
3. The installer leads in **French**; choose your language. You'll be asked to read and accept the licence and privacy policy — the accept box appears at the **end** of each document.
4. On finishing, MetawatchPHR starts and your browser opens to the dashboard with a built-in **demo patient** so you can explore immediately.

### Updating

Run the new installer right over your existing installation — no uninstall needed. If the app is running, approve **"Automatically close the applications"** when asked. Updates clean up the previous version's files automatically. **Your health records are never touched by an install, update, or even an uninstall** — they live in your own data folder, separate from the program.

### Privacy in one paragraph

*(Wording is legally load-bearing — change only with Legal.)* MetawatchPHR is fully local. No telemetry, no analytics, no cloud accounts. The software makes exactly **one** outbound network request beyond your own AI endpoint: a one-time licence-key validation when **you** paste a connector key — carrying only that key, never your data. Sending anything to an AI outside your machine requires your explicit, recorded consent, and the engine itself refuses without it.

### Known beta limitations

- The installer is **not yet code-signed** (the SmartScreen warning above).
- A scan shows **no progress indicator** yet — a long import can look idle while working. Check back; a completed scan shows its records on the timeline, and `scan_report.md` in the app's logs folder accounts for every file.
- **Image-only records** (e.g., a photographed X-ray) are not yet extracted — files must contain readable text or structured data.
- **macOS version:** built, in validation. **Linux:** planned.
- If something misbehaves: send us **one file** — `scan_report.md` from the app's logs folder. It lists what the scan saw and why, names no file contents, and refreshes each run (review it before sending).

### Connectors

The core product — import, records, charts, AI summaries — is **free forever**. Optional connectors for hospital-system exports are **$5 each or $10 for all, one-time, never a subscription**. Today **Epic** is active; purchased connectors keep working offline forever (we validate your key once and never phone home again).

---

*MetawatchPHR organizes and presents your own health information. It is not a medical device and does not provide diagnosis or medical advice — for clinical decisions, always consult a licensed healthcare professional.*

*MetawatchPHR — built by Metawatch. Windows beta available now; macOS coming. Support: `AI@Metawatch.ca`.*
