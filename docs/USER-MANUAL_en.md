<!-- CLASSIFICATION: PUBLIC · MetawatchPHR User Manual (EN) -->

# MetawatchPHR User Manual

**Document version:** v6.1 · **Last modified:** 2026-08-12
**Applies to:** MetawatchPHR 0.2.0, build `23ea06338668` ("V7c") · **Windows beta** (macOS release in preparation)

---

Welcome to **MetawatchPHR**, your personal, fully local health data refinery. MetawatchPHR takes your scattered, unstructured medical files — PDFs, Word documents, Excel spreadsheets, raw text, and hospital exports — and forges them into a unified, clinically coherent timeline that you can read, graph, and search.

This manual guides you through installation, adding users, configuring your local AI, daily operation, and the medical standards that power the system.

## 0. What you need before you start (system requirements)

- **Windows 10 or 11, 64-bit.** (The macOS version is in preparation; this beta is Windows only.)
- **[LM Studio](https://lmstudio.ai)** — a free application that runs the AI model locally on your machine. MetawatchPHR does its AI work through LM Studio so that nothing ever leaves your computer. See **Appendix A** for exact setup.
- **Enough memory for your chosen AI model.** LM Studio shows you whether a model fits your machine before you load it (see the model recommendations in Section 3).
- **Disk space** for the application (~a few hundred MB) plus room for your processed records.
- Nothing else — the installer bundles everything the application itself needs. You do not install Python, Node, or any other software.

## 1. Installation and Privacy Guarantees

MetawatchPHR is distributed as a standalone desktop application.

1. **Download the installer.** The filename looks like `MetawatchPHR-Setup-0.2.0-23ea06338668.exe`. The letters and numbers at the end identify your exact build — **if you ever report a problem, include that build code**; it tells us precisely which version you are running. If a download arrives smaller than expected, re-download directly rather than through a syncing folder — cloud drives can hand you a partial file.
2. **Expect a Windows warning — this is normal.** The beta installer is not yet code-signed, so Windows will warn you: SmartScreen shows *"Windows protected your PC"* (click **More info → Run anyway**), and User Account Control asks about an *"unknown publisher"* (click **Yes**). Code signing is planned; until then these warnings appear for every beta tester.

   ![The unknown-publisher prompt every beta tester sees — click Yes](manual-screenshots/shots/bonus_uac_unsigned_publisher.png)
3. **The installer runs in French first.** MetawatchPHR is built to Québec's language requirements, so the installer and the first-run screens present French by default. Choosing English is one click — and that choice is itself your agreement to proceed in English.

   ![The installer's language selection dialog — French presented first](manual-screenshots/shots/shot1_installer_language_fr.png)
4. **Accept the agreements — you must scroll to the end.** On first launch the application presents its two governing documents, one after the other: the **End-User License Agreement**, then the **Privacy Policy**. Each appears in full inside a scrollable reader, and its checkbox only becomes clickable **after you have scrolled to the end of the text**. If a checkbox looks greyed out, keep scrolling — that is the design, not a bug. Once both are acknowledged, the Accept button enables. A **consent receipt** recording what you accepted, in which language, is written to your data folder for your own records.

   ![The acceptance reader — scroll to the end of each document to enable its checkbox](manual-screenshots/shots/shot2_acceptance_reader.png)
5. **Your data environment is provisioned automatically** at `%LOCALAPPDATA%\OpenPHR` on Windows. *(Note: the folder carries the platform's internal name, OpenPHR — the product is MetawatchPHR. A future update aligns the folder name; your data is unaffected.)*
6. **First launch takes a few minutes.** The launcher opens a console window, prepares your data environment, and waits up to ~3 minutes for the local server on a cold start — **leave that window open while you use the app.** If your browser shows "can't reach this page" at first, give it a moment and refresh. If another program is already using the default port, MetawatchPHR automatically finds a free one.

   ![The launcher console — leave this window open; your browser opens when the app is ready](manual-screenshots/shots/bonus_launcher_console.png)

**Privacy — first and always.** MetawatchPHR is not cloud-hosted. Your health records never leave your machine. All AI processing runs against your local AI endpoint, and the system runs offline by default. In the standard configuration, the only network call ever made is a one-time license validation if you purchase a paid Connector — and that call contains zero health data.

**Meet the demo patient.** Every fresh install includes a built-in demonstration patient with synthetic records, so you can explore the timeline, charts, and search before scanning anything of your own. The demo patient is deliberately **read-only and cannot be deleted** — it is your permanent safe sandbox.

![The dashboard with the built-in demo patient — timeline, problems, and medications populated](manual-screenshots/shots/shot3_dashboard_demo_patient.png)

## 2. Setting Up and Adding a User

MetawatchPHR supports multiple users on a single machine with strict isolation between them. To set up a new user, add them explicitly to the User Roster:

1. **Open the Dashboard** — launch MetawatchPHR to open the browser dashboard.
2. **Navigate to Settings** — click the Settings gear icon.
3. **Open the User Roster page.**
4. **Click "Add User."**
5. **Fill in the user's details:**
   - **First and Last Name** — used to generate the internal identifier and to verify that extracted documents really belong to this user.
   - **Aliases** (optional) — nicknames, initials, or maiden names the AI should recognize as this user. Adding these improves matching on real-world documents.
6. **Set the Source Directory Path (CRITICAL)** — the folder on your computer where this user's raw medical files live (e.g., `C:\Users\You\Documents\HealthRecords`). The system scans **only** this directory for this user and strictly obeys the boundary — two users' data are never co-mingled. *(Tip: if you paste a path using Windows "Copy as path," it arrives wrapped in quotes — remove them.)*
7. **Save.** The system provisions a dedicated, secure folder for this user (`%LOCALAPPDATA%\OpenPHR\users\<identifier>`). All processed records permanently reside there.

![The User Roster — aliases, the source directory field, and Validate & Add](manual-screenshots/shots/shot4_user_roster_add_user.png)

## 3. Configuring the AI (LLM)

MetawatchPHR relies on an AI language model to extract structured clinical data from your unstructured files. By default it expects a **local, offline** model served by LM Studio, so zero data leaves your machine.

1. **Navigate to Settings → LLM panel.**
2. **Set the endpoint** — the URL of your local AI engine, normally `http://localhost:1234/v1/chat/completions`. You can also set the Model Name, Max Characters, and **Temperature — use `0.1`** (near-deterministic extraction with just enough flexibility for clinical summarization).
3. **Choose your model by platform:**
   - **Windows (this beta):** `Gemma 3 12B IT Q5_K_M` — excellent clinical reasoning with a moderate memory footprint, in the GGUF format LM Studio uses on Windows.
   - **Mac, 32 GB (upcoming release; our reference machine):** `mlx-community/gemma-4-26b-a4b-it` — the flagship model rigorously tested for maximum clinical precision. *(MLX models are Mac-only — Windows users should use the GGUF model above.)*
4. **Test Connection** — use the built-in button to validate that MetawatchPHR can reach your model before running a scan.

![The LLM Parameters panel — endpoint, Test Connection, and the LLM Enabled switch](manual-screenshots/shots/shot5_llm_parameters_panel.png)

**Security guard for external/cloud AI.** If you point MetawatchPHR at a cloud-hosted AI instead of a local one, a strict Consent Guard intervenes: the system detects the non-local URL, interrupts before saving, and presents a clear warning that sending medical records to an external service inherently risks your privacy. You must explicitly grant the external-processing consent for that specific host — or the change is blocked and your records stay on-device.

## 4. Daily Operation: The Scan Flow

1. **Start your local AI** — open LM Studio, load your model, start the server on port 1234 (Appendix A).
2. **Drop files** — place new medical documents into your Source Directory.
3. **Scan Now** — click the button in the dashboard. The system verifies the AI connection and begins processing.
4. **Read your receipt** — every scan writes a friendly report, `scan_report.md`, telling you which files were ingested, which were skipped and why (e.g., non-medical software files on a hospital disc), and which were quarantined for your review.

**What file types are supported:** PDF, Word, Excel/CSV, plain text, hospital C-CDA XML exports, and DICOM medical imaging (clinical tags and headers — with a built-in image viewer). **Not yet supported:** photographs of documents (e.g., a `.jpeg` of an X-ray or a paper record) — an extraction lane for images is on the roadmap.

**How long does it take?** The AI reads one document at a time, thoroughly. A handful of files takes minutes; a folder of hundreds of documents — or imaging discs with many files — can take hours. This is normal: the model is performing genuine clinical extraction on every page, on your own hardware. Leave it running; the report tells you everything it did.

**If something goes wrong, email ONE file to `AI@Metawatch.ca`:** `%LOCALAPPDATA%\OpenPHR\logs\scan_report.md` — it is written fresh on every run and starts with a review-before-sending note so you can check what's in it. Include your installer's build code (the letters/numbers in the installer filename). For deeper diagnosis we may also ask for `scan_run.log` from the same folder. *(Fittingly for this product, support is AI-staffed too.)*

## 5. Feature Deep-Dive

### Connectors (direct import lanes)
While the AI refinery is brilliant at reading unstructured text, some healthcare systems provide highly structured exports. Connectors are **deterministic, non-AI import lanes** for 100%-precision transcription:

- **Epic C-CDA (paid unlock)** — imports your entire Epic medical record (encounters, observations, labs) with zero AI involvement, using a static crosswalk that maps hospital codes into your ledger exactly. This lane works even if you have no AI model installed.
- **Apple Health** — arriving in a coming update: parses your `export.xml` (steps, resting heart rate, O2, and more) into canonical formats.
- **Cerner & OSCAR (CPAP)** — the architecture is wired for both; the import adapters arrive in later updates.

<!-- Screenshot pending re-capture. -->


### Graphing
The Patient Banner at the top of the dashboard houses interactive visualizations of your chronological data:

- **Biomarker Trends** — a selectable time-series chart of your lab results. Pick an analyte (e.g., Hemoglobin) and see your historical levels plotted against the standard reference-range band, making an out-of-bounds result instantly obvious.
- **Weight Trend** — a longitudinal chart of your weight over your clinical timeline.

### Search and Ledger Navigation
- **Global Search** — a powerful text search across your entire ledger; the domain filters nest with it so you can narrow to exactly the records you mean.
- **Record view** — click any clinical event to open the full structured record, including its provenance (where the data came from) and its integrity status. DICOM images open in the built-in viewer. *(Side-by-side viewing of the original source file is arriving in an update.)*
- **Quarantine** — documents the AI could not confidently attribute or date are never silently filed: they are quarantined, counted, and listed with reasons in your scan report. *(The in-app Review Queue screen for approving them is being finalized.)*

### SOAP Notes
MetawatchPHR turns messy medical visits into structured clinical prose. When the AI reads a transcript or doctor's note, it extracts into strict **SOAP** format — **S**ubjective (reported symptoms and history), **O**bjective (vitals, exam findings, labs), **A**ssessment (diagnoses), **P**lan (prescriptions, referrals, next steps) — transforming a jumbled 10-page document into a dense summary matching professional clinical rigor.

## 6. Medical Standards Implemented

MetawatchPHR is built rigorously on international medical-informatics standards, so your data is portable, clinically valid, and exact:

1. **FHIR R4** — the ledger is modeled after FHIR R4 constraints (`Patient`, `Observation`, `Encounter` resources).
2. **LOINC & UCUM** — all quantitative results are coded to canonical LOINC identifiers (e.g., `8867-4` for Heart Rate) and UCUM units, preventing duplicate metrics and enabling accurate graphing.
3. **C-CDA** — native parsing of the XML continuity-of-care documents exported by major hospital EHRs.
4. **DICOM** — machine-standard recognition of medical imaging files: clinical tags and headers are extracted safely via `pydicom` without executing or decoding image pixels.
5. **HL7v2** — structural recognition of standard hospital messaging formats.
6. **ICD-10 / SNOMED CT** — used under the hood to map diagnoses to universally recognized condition codes.

## 7. Uninstalling — and what happens to your data

- **Uninstalling removes the application only.** The uninstaller stops the app's own processes and removes the program folder. **It never touches your health records** — everything under `%LOCALAPPDATA%\OpenPHR` (your users, records, consent receipts, and logs) remains on your machine, by design. Reinstalling later finds your data exactly where you left it.
- **To remove your data completely,** delete the `%LOCALAPPDATA%\OpenPHR` folder yourself after uninstalling. That is deliberate: only you, by your own hand, can destroy your records.
- **Back up.** Your records live in that one folder — including a backup of it in whatever backup routine you already trust is strongly recommended.

![Your data folder — users, records, logs, and your consent receipts, all in one place](manual-screenshots/shots/bonus_data_home_folder.png)

---

## Appendix A: LM Studio Setup Guide

Configure LM Studio with these exact settings before clicking "Scan Now."

**1. Model selection** — download and load, by platform:
- **Windows (this beta):** `Gemma 3 12B IT Q5_K_M`
- **Mac, 32 GB (upcoming release):** `mlx-community/gemma-4-26b-a4b-it`

**2. Server configuration** — in the Local Server tab (`<->` icon):
- **Server Port:** `1234` (MetawatchPHR expects it here).
- **CORS:** toggled **ON** (lets the MetawatchPHR dashboard in your browser talk to the local server).

**3. Model parameters** — in the right-hand configuration panel:
- **Context Length:** minimum `40000`, recommended `50000` (dense medical documents need a large window to extract without truncation).
- **Temperature:** `0.1`.
- **GPU Offload:** Max / all available layers.
- **Keep Model in Memory:** ON (avoids reloading between scans).

Click **Start Server**, then use **Test Connection** in MetawatchPHR Settings to verify the wiring.

![LM Studio running with a Gemma-class model loaded and the local server reachable](manual-screenshots/shots/shot8_lmstudio_server.png)
