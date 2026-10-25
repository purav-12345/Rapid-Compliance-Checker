# Rapid-Compliance-Checker
### Intelligent Cross-Border Trade & Shipment Compliance

**An AI-assisted platform for researching shipment restrictions, checking prohibited goods, and navigating country-specific trade requirements.**

[![GitHub Repo](https://img.shields.io/badge/GitHub-Repository-181717?logo=github)](https://github.com/vvinayakkk/Logithon_IITB_Hackathon)
[![Live Demo](https://img.shields.io/badge/Live-Demo-2563eb?logo=vercel)](https://iitb-one.vercel.app/)
![Python](https://img.shields.io/badge/Python-Backend-3776AB?logo=python&logoColor=white)
![React](https://img.shields.io/badge/React-Web_UI-61DAFB?logo=react&logoColor=black)
![Hackathon](https://img.shields.io/badge/LogiTHON-IIT_Bombay-FF6B35)

[Overview](#overview) · [Features](#key-capabilities) · [Architecture](#architecture) · [Setup](#getting-started) · [Workflow](#example-compliance-workflow) · [Roadmap](#roadmap)

</div>

> **Project status:** Hackathon prototype. The functionality below is documented in the repository's original README. Some services, endpoints, model metrics, and integrations have not been independently validated. **The system is not a substitute for official customs or legal advice.**

## Overview

Cross-border shipments must comply with product restrictions, destination-country rules, carrier policies, and changing documentation requirements. Manually searching across government portals, carrier websites, and regulatory documents can be slow and inconsistent.

**TradeGuard AI** (originally titled **Rapid Compliance Checker**) explores a unified interface to support this work. The project brings together AI-assisted regulatory research, item identification, prohibited-goods checks, and automated compliance summaries.

**Developed for:** LogiTHON 2025, organized in the context of IIT Bombay's Industrial Engineering and Operations Research (IEOR) Day in collaboration with Softlink Global and partners.

**Live demo (repository-listed):** https://iitb-one.vercel.app/

## The Problem

- Shipping rules differ across destination countries and product categories.
- Operators often have to consult multiple sources to check whether an item is restricted.
- Manual handling of high-volume shipment records is difficult to scale.
- Non-specialists need understandable explanations and links to authoritative sources.

## Key Capabilities

The original project documentation describes the following modules:

| Module | Intended experience | Documented technology / technique |
|---|---|---|
| Regulatory knowledge base | Ask about country-specific shipping requirements | Graph retrieval-augmented generation (Graph RAG) |
| Prohibited-item checks | Search by product or destination country | Country/item matching and rule lookup |
| Image-based inspection | Upload a product image to identify possible items | YOLOv11 oriented bounding-box (OBB) object detection |
| Bulk shipment checks | Submit multiple shipment entries in a CSV file | Batch processing / service architecture |
| AI assistant | Ask follow-up questions about shipment restrictions | Conversational AI with context |
| AI research agents | Gather and summarize regulatory information | Agentic workflows and web research |
| Reporting and sharing | Export findings and communicate them to stakeholders | PDF, CSV, email, SMS / WhatsApp integrations described |
| Accessibility | Provide assistance in multiple languages | Multilingual support described |
| Adaptive analysis | Experiment with feedback-driven compliance guidance | Reinforcement learning module |

> The source README reports a **99.2% detection accuracy** for an image model and checks against **22+ FedEx rules**. These figures are **project-reported**, with no accessible reproducible evaluation protocol here; do not treat them as independently verified benchmarks.

## Architecture

```mermaid
flowchart TB
    A[Importer / Exporter / Logistics User] --> B[Web Client]
    B --> C[Backend Services]
    C --> D[Country & Item Restriction Lookup]
    C --> E[AI Regulatory Q&A / Graph RAG]
    C --> F[Image Detection / YOLOv11 OBB]
    C --> G[Batch Shipment Analysis]
    C --> H[Reports & Notifications]
    D --> I[(Compliance Rules / Data Sources)]
    E --> I
    E --> J[Agentic Web Research]
    F --> K[Identified Items]
    G --> D
    D --> L[Results with Sources & Review Flags]
    E --> L
    K --> L
    H --> L
    L --> B
```

*Conceptual diagram derived from the existing README; it does not certify that each connection is present or operational in the current code.*

### High-Level Technology Stack

| Layer | Technology described in existing documentation |
|---|---|
| Frontend | React (the original README also references Vue.js; verify the actual client implementation) |
| Backend | Python, Flask |
| Database | MongoDB |
| AI and retrieval | Graph RAG, AI agents / CrewAI |
| Computer vision | YOLOv11 OBB |
| Learning experiments | Reinforcement learning |
| Notifications | Twilio, email-related services |
| Mobile | React Native (documented; verify actual mobile application entry point) |
| Deployment | A Vercel-hosted demo URL is linked in the repository |

## Repository Structure

The following top-level directories were visible in the public repository:

```text
Logithon_IITB_Hackathon/
├── anushka/
├── client/                 # Client-side application (inspect package.json)
├── harshit/
├── harshit2/
├── harshit3/
├── myapp/
├── reinforcement_agent/    # Reinforcement-learning-related module
├── server/                 # Server-side application (verify startup file)
├── vinayak/
├── vinayak2/
├── .gitignore
├── README.md
├── package-lock.json
└── requirements.txt
```

The named team directories are retained exactly as committed. Their internal modules and entry points should be documented after inspecting their contents; directory labels above are not assertions about unreviewed code.

## Getting Started

### Prerequisites

- Git
- Python 3 and `pip`
- Node.js and `npm`, if the `client/` package uses them
- Credentials for any configured external AI, messaging, database, or regulatory data providers

### 1. Clone the actual repository

```bash
git clone https://github.com/vvinayakkk/Logithon_IITB_Hackathon.git
cd Logithon_IITB_Hackathon
```

### 2. Create the Python environment

```bash
python -m venv .venv
# macOS / Linux:
source .venv/bin/activate
# Windows PowerShell:
# .venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

> This installs the root dependency list; individual team services may have additional requirements. Check the service folders for their own requirements or configuration before running them.

### 3. Start the backend service

Inspect `server/` (and any related team directories) to determine the actual Flask entry point and required environment variables. **No single verified startup command is available from the accessible top-level files.** Once identified, run the corresponding service according to its source configuration.

### 4. Start the web client

If `client/package.json` is present and contains the expected scripts:

```bash
cd client
npm install
npm run dev
```

If `dev` is not defined, use the appropriate script shown by `npm run`. The root `package-lock.json` is minimal and should not be treated as the client's dependency manifest.

### 5. Set configuration securely

Create local `.env` files only where the code reads them, for example:

```dotenv
# Illustrative variable names only — match them to the implementation
MONGODB_URI=<your-database-connection>
AI_API_KEY=<your-provider-key>
TWILIO_ACCOUNT_SID=<your-sid>
TWILIO_AUTH_TOKEN=<your-token>
```

Do **not** commit API keys, database passwords, shipping account credentials, or private shipment data. Update `.gitignore` as needed. Variable names here are examples, not verified application contracts.

## Example Compliance Workflow

```mermaid
sequenceDiagram
    actor User as Shipment Operator
    participant UI as Web Interface
    participant API as Compliance Backend
    participant Rules as Regulatory Sources
    participant AI as AI Analysis Modules
    User->>UI: Enter destination and product details
    UI->>API: Request compliance assessment
    API->>Rules: Retrieve relevant restrictions
    Rules-->>API: Rules and source metadata
    API->>AI: Explain / classify potential issues
    AI-->>API: Assessment and flagged uncertainties
    API-->>UI: Results with caveats and references
    UI-->>User: Review shipment guidance
```

**Example questions the platform is intended to support:**

- Can this product be shipped to a specified destination?
- Which countries restrict a selected category of goods?
- Which documents or checks might be required?
- Which shipments in a bulk upload need manual review?

**Important:** An AI-generated response is a preliminary screening aid. Always confirm regulatory requirements with the destination country's official customs authority and relevant carriers before shipping.

## Screenshots & Demo

**Demo:** [Open the application](https://iitb-one.vercel.app/)

Add real screenshots under an `assets/screenshots/` directory and replace the placeholders below:

| Screen | Suggested file | What to demonstrate |
|---|---|---|
| Landing page | `assets/screenshots/home.png` | Product purpose and navigation |
| Prohibited-item search | `assets/screenshots/item-check.png` | Country/item restrictions |
| Image analysis | `assets/screenshots/image-analysis.png` | Upload and detected objects |
| Bulk checks | `assets/screenshots/bulk-check.png` | CSV upload and results |
| Compliance chat | `assets/screenshots/assistant.png` | Answer with cited source |

Example after adding screenshots:

```markdown
![TradeGuard dashboard](assets/screenshots/home.png)
```

## Responsible Use & Limitations

- Regulations change frequently; include the source URL and retrieval date in any compliance report.
- A model-detected object is not necessarily the correct customs classification or HS code.
- Carrier restrictions and government import/export laws are separate requirements.
- Low-confidence, conflicting, or unavailable rules should trigger manual review rather than automatic approval.
- The original project's performance claims need a reproducible dataset, evaluation script, and test conditions before being cited as established results.
- This repository's accessible files do not establish compliance certification, regulatory approval, or production-grade security.

## Suggested Evaluation

| Area | Useful metric |
|---|---|
| Prohibited-item retrieval | Precision, recall, source coverage |
| Country-rule freshness | Time since authoritative source update |
| Vision model | Per-class precision/recall, mAP on held-out images |
| AI explanations | Grounding accuracy, citation correctness |
| Bulk operations | Records per minute, failure rate |
| User experience | Task completion rate and manual-review rate |

## Roadmap

- [ ] Verify and document exact service entry points, ports, and environment variables.
- [ ] Add automated tests for rules, endpoints, and CSV ingestion.
- [ ] Attach official source URLs and timestamps to every compliance result.
- [ ] Publish model cards and reproducible evaluation for image detection and retrieval.
- [ ] Add role-based access controls and secure audit logs.
- [ ] Add end-to-end tests for bulk shipment workflows.
- [ ] Provide a reproducible containerized deployment configuration.
- [ ] Add dashboard screenshots and a short product demo.

## Contributing

Contributions and documentation improvements are welcome through issues and pull requests. Please avoid submitting private shipment records, credentials, or other sensitive customer information.

## Attribution

Developed as a **LogiTHON / IIT Bombay hackathon project**. The GitHub repository originally calls this application **Rapid Compliance Checker**; **TradeGuard AI** is a suggested name for clearer GitHub portfolio branding.

## License

No root-level `LICENSE` file was visible in the inspected repository listing. The original README references MIT, but verify licensing and add an actual `LICENSE` file before claiming a legally operative open-source license.

---

<div align="center"><strong>TradeGuard AI</strong> — Turning fragmented shipping rules into understandable, reviewable decisions.</div>
